# Puppet-conf

## Description
This is a basic puppet config that utilizes hiera and r10k.

## Basic Requirements
* Ubuntu 14
* Ruby 1.9.2 or higher

## Installation
To install follow the steps below.
Ideally you will want to use Packer to bake this into an AMI(Tested).

### Install Ruby
Needed by puppet and r10k.
```
apt-get install ruby 
```

### Install Git
Needed so that you can fetch codes from git repos.
Generate a key and add associate it to your account.
```
apt-get install git
```

### Install Puppet
```
wget http://apt.puppetlabs.com/puppetlabs-release-trusty.deb
dpkg -i /tmp/puppetlabs-release-trusty.deb
apt-get update
apt-get install ruby puppet git
```

### Install r10k
```
gem install r10k
```

## Configuration
You can fetch base configuration from;
```
git@git.freelancer.com:reilly/puppet-conf.git
```

Basically remove the existing puppet configuration and replace it.
```
rm -rf /etc/puppet
git clone git@git.freelancer.com:reilly/puppet-conf.git /etc/puppet
```

## r10k Usage

### Deploying Environments
Recursively update all environments:
```
r10k deploy environment --puppetfile
```

Update environments while avoiding unnecessary recursion:
```
r10k deploy environment
```

Update a single environment:
```
r10k deploy environment development
```

Update a single environment and force an update of modules:
```
r10k deploy environment my_working_environment --puppetfile
```

### Deploying Modules
Update a single module across all environments:
```
r10k deploy module stdlib
```

Update multiple modules across all environments:
```
r10k deploy module ntp stdlib
```

Update one or more module in a single environment:
```
r10k deploy module -e development ntp stdlib
```

### Viewing Environments
Display all environments being managed by r10k:
```
r10k deploy display
```

Display all environemnts being managed by r10k and modules specified in the Puppetfile:
```
r10k deploy display -p
```

Display all environments being managed by r10k, and modules specified in the Puppetfile along with their expected and actual versions:
```
r10k deploy display -p --detail
```

Display an explicit list of environments being managed by r10k and modules specified in the Puppetfile along with their expected and actual versions:
```
r10k deploy display -p --detail production ntp stdlib
```

## Puppet Usage

### Run puppet

Running puppet on target environment:
```
puppet apply /etc/puppet/environments/development/site.pp
```

