# Cookbook: mo_backup_sample

Sample application used to show how to use
[mo_backup](https://github.com/Desarrollo-CeSPI/mo_backup) cookbook.

## Table of Contents

* [Attributes](#attributes)
* [Data bags](#data-bags)
* [Recipes](#recipes)
* [Usage](#usage)
* [To Do](#to-do)
* [License](#license)
* [Authors](#authors)

## Attributes

The following attributes are keys of a hash inside
`default["mo_backup_sample"]["backup"]`. Check attributes/defaults.rb.

`id`: application id.
`description`: an application description.
`user`: the user the application runs with.
`databag`: the databag where the application is defined.
`storages_databag`: databag where different storages are defined.
`mail_databag`: databag where mailservers and accounts are defined.

**Important**: every databag used in this recipe is encrypted with the key
stored in sample/.chef/data_bag_key.

## Data bags

There are several databags, located inside sample/data_bags. There, application
configuration, storages and mail relay configuration are defined. 

To view or edit the encrypted data bags you will need to first install the
following gems:

* [Knife solo](http://matschaffer.github.io/knife-solo/)
* [Knife solo data bag](https://github.com/thbishop/knife-solo_data_bag)

After that, you will be able to execute the following commands (make sure you
run these commands inside sample directory):

```
knife solo data bag edit applications my_app --secret-file .chef/data_bag_key
knife solo data bag show mail_databag mail_app --secret-file .chef/data_bag_key
```

## Recipes

The only recipe this cookbook includes is `backup`, which uses mo_backup to
write a custom backup file inside the application's home user directory. By
default, that file will be named .backup_my_app_production, which is the result
of the string backup, the application id and the environment.

## Usage

To use this recipe just run `vagrant up` and it should work.

## To Do

This cookbook uses mo_backup and that one has not yet implemented a task to add
cron jobs so this cookbook will create and write the backup configuration file
but will not schedule it to be executed periodically. Besides, this cookbook
does not install the backup gem required.

## License

The MIT License (MIT)

Copyright (c) 2014 Christian Rodriguez & Leandro Di Tommaso

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.

## Authors

* Author:: Christian Rodriguez (chrodriguez@gmail.com)
* Author:: Leandro Di Tommaso (leandro.ditommaso@mikroways.net)
