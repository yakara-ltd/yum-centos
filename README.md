yum-centos Cookbook
============

The yum-centos cookbook takes over management of the default
repositoryids that ship with CentOS systems. It allows attribute
manipulation of base updates extras centosplus contrib.

Requirements
------------
* Chef 11 or higher
* yum cookbook version 3.0.0 or higher

Attributes
----------
The following attributes are set by default

``` ruby
default['yum']['base']['repositoryid'] = 'base'
default['yum']['base']['mirrorlist'] = 'http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os'
default['yum']['base']['description'] = 'CentOS-$releasever - Base'
default['yum']['base']['enabled'] = true
default['yum']['base']['gpgcheck'] = true
default['yum']['base']['gpgkey'] = 'file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6'
```

``` ruby
default['yum']['contrib']['repositoryid'] = 'contrib'
default['yum']['contrib']['description'] = 'CentOS-$releasever - Contrib'
default['yum']['contrib']['mirrorlist'] = 'http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=contrib'
default['yum']['contrib']['enabled'] = false
default['yum']['contrib']['gpgcheck'] = true
default['yum']['contrib']['gpgkey'] = 'file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6'
```

``` ruby
default['yum']['extras']['repositoryid'] = 'extras'
default['yum']['extras']['description'] = 'CentOS-$releasever - Extras'
default['yum']['extras']['mirrorlist'] = 'http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=extras'
default['yum']['extras']['enabled'] = true
default['yum']['extras']['gpgcheck'] = true
default['yum']['extras']['gpgkey'] = 'file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6'
```

``` ruby
default['yum']['centosplus']['repositoryid'] = 'centosplus'
default['yum']['centosplus']['description'] = 'CentOS-$releasever - Centosplus'
default['yum']['centosplus']['mirrorlist'] = 'http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=centosplus'
default['yum']['centosplus']['enabled'] = false
default['yum']['centosplus']['gpgcheck'] = true
default['yum']['centosplus']['gpgkey'] = 'file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6'
```

``` ruby
default['yum']['updates']['repositoryid'] = 'updates'
default['yum']['updates']['description'] = 'CentOS-$releasever - Updates'
default['yum']['updates']['mirrorlist'] = 'http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=updates'
default['yum']['updates']['enabled'] = true
default['yum']['updates']['gpgcheck'] = true
default['yum']['updates']['gpgkey'] = 'file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6'
```

Recipes
-------
* default - Walks through each of the following attributes and feeds a
  yum_resource parameters based on node attributes. 

  yum_repository 'base' do
    mirrorlist 'http://mirrorlist.centos.org/?release=$releasever&arch=$basearch&repo=os'
    description 'CentOS-$releasever - Base'
    enabled true
    gpgcheck true
    gpgkey 'file:///etc/pki/rpm-gpg/RPM-GPG-KEY-CentOS-6'
  end
  
Usage Example
-------------
To disable the CentOS Extras repository through a Role or Environment definition

```
default_attributes(
  :yum => {
    :extras => {
      :enabled => {
        false
       }
     }
   }
 )
```

To enable the CentOS Plus repository with a wrapper cookbook, place
the following in a recipe:

```
node.default['yum']['centosplus']['enabled'] = true
include_recipe 'yum-centos'
```

More Examples
-------------
Point the base and updates repositories at an internally hosted server.

```
node.default['yum']['base']['enabled'] = true
node.default['yum']['base']['mirrorlist'] = nil
node.default['yum']['base']['baseurl'] = 'https://internal.example.com/centos/6/os/x86_64'
node.default['yum']['base']['sslverify'] = false
node.default['yum']['updates']['enabled'] = true
node.default['yum']['updates']['mirrorlist'] = nil
node.default['yum']['updates']['baseurl'] = 'https://internal.example.com/centos/6/updates/x86_64'
node.default['yum']['updates']['sslverify'] = false

include_recipe 'yum-centos'
```

License & Authors
-----------------
- Author:: Sean OMeara (<someara@opscode.com>)

```text
Copyright:: 2011-2013 Opscode, Inc.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```
