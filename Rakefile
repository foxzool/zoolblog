# Andrew Disley: Front-end Skeleton
# http://github.com/andrewdisley/front-end-skeleton

task :default => :build

def windows?
  Config::CONFIG['host_os'] =~ /mswin/
end

desc 'Jekyll build'
task :build do
  jekyll
end

desc 'Jekyll --auto'
task :auto do
  jekyll('--auto')
end

desc 'Jekyll --server --auto --pygments'
task :server do
  jekyll('--server --auto --pygments')
end

desc 'Deploy to staging'
task :staging do
  jekyll
#  sh 'rsync -rtzhv --delete _site/ server:/home/user/sites/domain.ext/public/'
end

desc 'Deploy to live, replaces live server with _site'
task :live do
  jekyll
  sh 'rsync -rtzhv --delete _site/ zool@zool.me::zoolme'
end

def jekyll(opts = '')
  if windows?
    sh 'rmdir /s /q _site'
    sh 'mkdir _site'
  elsif
    sh 'rm -rf _site'
  end
  sh 'jekyll ' + opts
end