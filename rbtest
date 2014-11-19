#!/usr/bin/env ruby

DEFAULT_FILES = ['test']

if i = ARGV.index('--')
  files = ARGV.first(i)
  args = ARGV[i+1..-1]
else
  files = ARGV
  args = []
end

n_in = files.size
files = DEFAULT_FILES.select { |f| File.exist?(f) } if files.empty?
files = files.flat_map { |f| File.directory?(f) ? Dir[f + '/**/*_test.rb'] : f }
n_actual = files.size

print "# %s: n_in = %p, n_actual = %p\n\n" % [File.basename($0), n_in, n_actual]

exec 'bundle', 'exec', 'ruby', \
  '-e', 'ARGV.each { |f| break if f =~ /^-/; load f }', \
  '--', *files, '--pride', *args
