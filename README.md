yum-erlang_solutions Cookbook
============

The yum-erlang_solutions cookbook takes over management of the default
repositoryids used by erlang_solutions. It allows attribute manipulation of
`erlang_solutions`.

Requirements
------------
* Chef 11 or higher
* yum cookbook version 3.0.0 or higher

Attributes
----------
The following attributes are set by default

``` ruby
default['yum']['erlang_solutions']['baseurl'] = 'http://packages.erlang-solutions.com/rpm/centos/$releasever/$basearch'
default['yum']['erlang_solutions']['description'] = 'Centos $releasever - $basearch - Erlang Solutions'
default['yum']['erlang_solutions']['gpgkey'] = 'http://packages.erlang-solutions.com/debian/erlang_solutions.asc'
default['yum']['erlang_solutions']['enabled'] = true
```

Recipes
-------
* default - Walks through node attributes and feeds a yum_resource
  parameters. The following is an example a resource generated by the
  recipe during compilation.

```ruby
  yum_repository 'erlang_solutions' do
    baseurl 'http://packages.erlang-solutions.com/rpm/centos/$releasever/$basearch'
    description 'Centos $releasever - $basearch - Erlang Solutions'
    enabled true
    gpgcheck true
    gpgkey 'http://packages.erlang-solutions.com/debian/erlang_solutions.asc'
  end
```

Usage Example
-------------
To disable the erlang_solutions repository through a Role or Environment definition

```
default_attributes(
  :yum => {
    :erlang_solutions => {
      :enabled => {
        false
       }
     }
   }
 )
```

To enable the erlang_solutions repository with a wrapper cookbook, place
the following in a recipe:

```
node.default['yum']['erlang_solutions']['enabled'] = true
include_recipe 'yum-erlang_solutions'
```

More Examples
-------------
Point the erlang_solutions repositories at an internally hosted server.

```
node.default['yum']['erlang_solutions']['enabled'] = true
node.default['yum']['erlang_solutions']['baseurl'] = 'https://internal.example.com/erlang_solutions'
node.default['yum']['erlang_solutions']['sslverify'] = false

include_recipe 'yum-erlang_solutions'
```

License & Authors
-----------------
- Author:: Sean OMeara (<someara@chef.io>)

```text
Copyright:: 2011-2013 Chef Software, Inc.

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
