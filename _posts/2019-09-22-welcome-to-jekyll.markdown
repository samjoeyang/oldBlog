---
layout: post
title:  "Welcome to Jekyll!"
date:   2019-09-22 18:01:41 +0800
categories: jekyll update
---
You’ll find this post in your `_posts` directory. Go ahead and edit it and re-build the site to see your changes. You can rebuild the site in many different ways, but the most common way is to run `jekyll serve`, which launches a web server and auto-regenerates your site when a file is updated.

Jekyll requires blog post files to be named according to the following format:

`YEAR-MONTH-DAY-title.MARKUP`

Where `YEAR` is a four-digit number, `MONTH` and `DAY` are both two-digit numbers, and `MARKUP` is the file extension representing the format used in the file. After that, include the necessary front matter. Take a look at the source for this post to get an idea about how it works.

Jekyll also offers powerful support for code snippets:

{% highlight ruby %}
def print_hi(name)
  puts "Hi, #{name}"
end
print_hi('Tom')
#=> prints 'Hi, Tom' to STDOUT.
{% endhighlight %}

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/

迁移过程：
# 1.安装环境
```
apt-get install ruby-full build-essential zlib1g-dev

echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

gem install jekyll bundler
```
Look Here: https://jekyllrb.com/

# 2. 从wordpress导出文章
Look here:https://segmentfault.com/a/1190000013962257
## 2.1 安装支持
```
apt-get install libmysqlclient-dev
gem install jekyll-import sequel unidecode mysql2 htmlentities
```
## 2.2 运行
```
ruby -r rubygems -e 'require "jekyll-import";
    JekyllImport::Importers::WordPress.run({
      "dbname"         => "dbname",
      "user"           => "dbuser",
      "password"       => "dbpassword",
      "host"           => "localhost",
      "port"           => "3306",
      "socket"         => "/var/run/mysqld/mysqld.sock",
      "table_prefix"   => "wp_",
      "site_prefix"    => "",
      "clean_entities" => true,
      "comments"       => true,
      "categories"     => true,
      "tags"           => true,
      "more_excerpt"   => true,
      "more_anchor"    => true,
      "extension"      => "html",
      "status"         => ["publish"]
    })'
```
导出成功后自行做一些文本替换例如
```
sed -i 's/email: email@example.com/email: youremail@example.com/g' *.html
```
## 2.3 导出成功后编译
```
jekyll b
```
注意：可能出现报错，因为“{}”引起问题，删除{}即可

# 3.提交到Github上
关于github的配置，自行搜索
