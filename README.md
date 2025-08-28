# password_generator.rb

class PasswordGenerator
  LETTERS = ('a'..'z').to_a + ('A'..'Z').to_a
  NUMBERS = ('0'..'9').to_a
  SYMBOLS = %w[! @ # $ % ^ & * ( ) - _ + = ?]

  def initialize(length = 12, use_symbols = true)
    @length = length
    @use_symbols = use_symbols
  end

  def generate
    pool = LETTERS + NUMBERS
    pool += SYMBOLS if @use_symbols

    Array.new(@length) { pool.sample }.join
  end
end

# CLI
puts "=== Password Generator ==="
print "Enter password length (default 12): "
length = gets.chomp.to_i
length = 12 if length <= 0

print "Include symbols? (y/n, default y): "
include_symbols = gets.chomp.downcase
use_symbols = include_symbols.empty? || include_symbols == "y"

generator = PasswordGenerator.new(length, use_symbols)
password = generator.generate

puts "\nGenerated Password: #{password}"
