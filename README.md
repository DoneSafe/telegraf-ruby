# Telegraf

Minimal gem to send metrics to a local telegraf agent.

This gem only uses the line protocol from the `influxdb` gem and does not depend on a specific version. This may break in the future but does not restrict you in using a your preferred `influxdb` version.

## Installation

```ruby
gem 'telegraf'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install telegraf

## Usage

Configure telegraf socket listener e.g.:

```
[[inputs.socket_listener]]
  service_address = "udp://localhost:8094"

```

```ruby
telegraf = Telegraf::Agent.new 'udp://localhost:8094'
telegraf = Telegraf::Agent.new # default: 'udp://localhost:8094'

telegraf.write('demo',
    tags: {tag_a: 'A', tag_b: 'B'},
    values: {value_a: 1, value_b: 1.5})

telegraf.write([{
    series: 'demo',
    tags: {tag_a: 'A', tag_b: 'B'},
    values: {value_a: 1, value_b: 1.5}
}])
```

There is not buffer or batch handling, nor connection pooling or keep alive. Each `#write` creates a new connection (unless it's a datagram connection).

There is no exception handling.

## License

Copyright (C) 2017-2020 Jan Graichen

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the GNU General Public License for more details.

You should have received a copy of the GNU Lesser General Public License along with this program.  If not, see <http://www.gnu.org/licenses/>.
