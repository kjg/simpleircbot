#!/usr/bin/env ruby

require 'socket'

class SimpleIrcBot

  def initialize(server, port, channel)
    @channel = channel
    @socket = TCPSocket.open(server, port)
    say "NICK IrcBot"
    say "USER ircbot 0 * IrcBot"
    say "JOIN ##{@channel}"
    say_to_chan "#{1.chr}ACTION is here to help#{1.chr}"
  end

  def say(msg)
    puts msg
    @socket.puts msg
  end

  def say_to_chan(msg)
    say "PRIVMSG ##{@channel} :#{msg}"
  end

  def run
    until @socket.eof? do
      msg = @socket.gets
      puts msg

      if msg.match(/^PING :(.*)$/)
        say "PONG #{$~[1]}"
        next
      end

      if msg.match(/PRIVMSG ##{@channel} :(.*)$/)
        content = $~[1]

        #put matchers here
        if content.match()
          say_to_chan('your response')
        end
      end
    end
  end

  def quit
    say "PART ##{@channel} :Daisy, Daisy, give me your answer do"
    say 'QUIT'
  end
end

bot = SimpleIrcBot.new("irc.freenode.net", 6667, 'ChannelName')

trap("INT"){ bot.quit }

bot.run
