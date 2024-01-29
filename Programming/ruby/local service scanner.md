# local service scanner
```text-x-ruby
require 'etc'

TCP_STATES = { # /usr/src/linux/include/net/tcp_states.h
  '00': 'UNKNOWN',
  'FF': 'UNKNOWN',
  '01': 'ESTABLISHED',
  '02': 'SYN_SENT',
  '03': 'SYN_RECV',
  '04': 'FIN_WAIT1',
  '05': 'FIN_WAIT2',
  '06': 'TIME_WAIT',
  '07': 'CLOSE',
  '08': 'CLOSE_WAIT',
  '09': 'LAST_ACK',
  '0A': 'LISTEN',
  '0B': 'CLOSING',
  '0C': 'NEW_SYN_RECV'
}

def decode_addr(addr)
  ip, port = addr.split(':')
  ip = ip.scan(/.{2}/).map{|x|x.hex.to_s}.reverse.join('.')
  port = port.hex.to_s
  "#{ip}:#{port}"
end

puts 'local address'.ljust(22) + 'remote address'.ljust(22) + 'state'.ljust(12) + 'username (uid)'
File.readlines('/proc/net/tcp').each_with_index do |line, i|
  entry = line.split(' ')
  unless i == 0 # skip headers
    laddr = decode_addr(entry[1])
    raddr = decode_addr(entry[2])
    state = TCP_STATES[entry[3].to_sym]
    uid = entry[7]
    uname = Etc.getpwuid(uid.to_i).name
    puts "#{laddr.ljust(22)}#{raddr.ljust(22)}#{state.ljust(12)}#{uname} (#{uid})"
  end
end
```