= rubyrep

== MISSION:

Development of an open-source solution for asynchronous, master-master replication of relational databases that is
* ridiculously easy to use
* database independent

== CONFIGURATION:

```rubyrep.conf
RR::Initializer::run do |config|
  config.left = {
    :adapter  => 'postgresql', # or 'mysql'
    :database => 'db1',
    :username => 'postgres',
    :password => '',
    :host     => 'db',
    :schema_search_path => 'public'
  }

  config.right = {
    :adapter  => 'postgresql',
    :database => 'db1',
    :username => 'postgres',
    :password => '',
    :host     => 'db2',
    :schema_search_path => 'public'
  }

  config.options[:sequence_adjustment_buffer] = 2
  config.options[:sequence_increment] = 10
  config.options[:scan_progress_printer] = :scan_progress_printers
  config.options[:database_connection_timeout] = 10
  config.options[:sync_conflict_handling] = :left_wins
  config.options[:replication_conflict_handling] = :left_wins
  config.options[:replication_interval] = 5
  # config.add_table_options 'emp', 
  #   :sync_conflict_handling => :left_wins,
  #   :replication_conflict_handling => :left_wins
  config.include_tables /./ # all tables

  # ------ exclude tables ------
  config.exclude_tables 'dontsynctable'
end

```


== MORE INFORMATION:

Refer to the project website at http://www.rubyrep.org

== LICENSE:

(The MIT License)

Copyright (c) 2017 Arndt Lehmann

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
