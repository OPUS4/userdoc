# -*- mode: ruby -*-
# vi: set ft=ruby :

$ruby = <<SCRIPT
apt-get update
apt-get -y install ruby-full build-essential zlib1g-dev

if ! grep "Install Ruby" /home/vagrant/.bashrc > /dev/null; then
  echo '# Install Ruby Gems to ~/gems' >> /home/vagrant/.bashrc
  echo 'export GEM_HOME="$HOME/gems"' >> /home/vagrant/.bashrc
  echo 'export PATH="$GEM_HOME/bin:$PATH"' >> /home/vagrant/.bashrc
  echo 'export BUNDLE_PATH="$HOME/bundles"' >> /home/vagrant/.bashrc
  echo 'alias runsite="bundle exec jekyll serve --host 0.0.0.0"' >> /home/vagrant/.bashrc
fi

source /home/vagrant/.bashrc

gem install bundler jekyll jekyll-sitemap
SCRIPT

$jekyll = <<SCRIPT
cd /vagrant
bundle update
SCRIPT

$environment = <<SCRIPT
if ! grep "cd /vagrant" /home/vagrant/.profile > /dev/null; then
  echo "cd /vagrant" >> /home/vagrant/.profile
fi
SCRIPT

$help = <<SCRIPT
echo 'Log into the VM using "vagrant ssh".'
echo 'Run Jekyll with "runsite" or "runsite --incremental".'
echo 'You can then access the site in your browser using:'
echo 'http://localhost:4000/userdoc/'
SCRIPT

Vagrant.configure("2") do |config|
  config.vm.box = "bento/ubuntu-22.04"

  config.vm.network "forwarded_port", guest: 4000, host: 4000

  config.vm.provision "shell", inline: $ruby
  config.vm.provision "shell", privileged: false, inline: $jekyll, env: {:BUNDLE_PATH => '$HOME/bundles'}
  config.vm.provision "shell", inline: $environment
  config.vm.provision "shell", run: "always", inline: $help
end
