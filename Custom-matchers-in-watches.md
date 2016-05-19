# Using custom matchers in watches

## Intro

A `watch` statement filters files that changed to match the given regexp.

Since Guard 2.14.x, you can pass a custom matcher if it has the right methods.

This allows you to create powerful rules without complex and unreadable hacks.

## Example

Lets say you want to respond only to changes in uncommitted files. 

You might have:

```ruby
only_uncommitted_lib_files = MyGitModifiedMatcher.new
watch(only_uncommitted_lib_files) { |m| "spec/#{m[:path_without_ext]}_spec.rb" }
```

A pseudo-implementation of the `MySpecialMatcher` class would be:

```ruby
class MyGitModifiedMatcher
  class MyMatchData
    def initialize(result)
      @result = result
    end

    def to_a
      @result.values
    end

    def [](name)
      @result[name]
    end
  end

  def match(filename_or_pathname)
    return nil unless `git status -uno`.lines.map(&:chomp).include?(filename_or_pathname)
    MyMatchData.new(path_without_ext: File.basename(file,File.extname(file)))
  end
end
```

Feel free to open an issue to discuss improvements.