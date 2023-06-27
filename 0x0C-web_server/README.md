# This manifest installs ngix and adds redirect page

package {'nginx':
  ensure => present,
  name   => 'nginx',
}

file {'/var/www/html/index.html':
  ensure  => present,
  path    => '/var/www/html/index.html',
  content => 'Hello World!',
}

file_line { 'redirect_me':
  ensure => present,
  path   => '/etc/nginx/sites-available/default',
  after  => 'listen 80 default_server;',
  line   => 'rewrite ^/redirect_me https://www.youtube.com/watch?v=QH2-TGUlwu4 permanent;',
}

service { 'nginx':
  ensure     => running,
  hasrestart => true,
  require    => Package['nginx'],
  subscribe  => File_line['redirect_me'],
}

A web server is software and hardware that uses HTTP (Hypertext Transfer Protocol) and other protocols to respond to client requests made over the World Wide Web. The main job of a web server is to display website content through storing, processing and delivering webpages to users
