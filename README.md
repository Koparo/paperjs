# Paperjs

Welcome to your new gem! In this directory, you'll find the files you need to be able to package up your Ruby library into a gem. Put your Ruby code in the file `lib/paperjs`. To experiment with that code, run `bin/console` for an interactive prompt.

This gem bundles the upstream distribution for use with the Ruby on Rails framework. The version number of
the gem always tracks the upstream javascript release and the gem itself doesn't provide any additional
methods or helpers. If a need for helpers arises in the future they will be developed as a separate gem
with this one as its dependency. Should a gem bug be discovered an additional version identifier will be
appended and incremented after the upstream version number.

## License
paperjs gem and changes made to paper.js required for rails are licensed under ISC.

The original paper.js code distributed with this gem is licensed under [MIT](https://tldrlegal.com/license/mit-license)
You can find the paper.js license file in the vendor directory, changes made to the original code base are as follows:

 - none so far

## Installation

Add this line to your application's Gemfile:

```ruby
gem 'paperjs'
```

And then execute:

    $ bundle

Or install it yourself as:

    $ gem install paperjs

## Usage

If you want to just use the Javascript paper.js API without paperscript support add the following in `application.js`:

    //= paperjs-core

If you wish to user paperscript in your rails application include the following instead:

    //= paperjs-full

Paperscript files should be included as type text/paperscript, you can set up the rails asset pipeline to handle
this without mixing your paperscript and javacsript files.

Create a new folder `app/assets/paperscripts` and add it to `config/initializers/assets.rb`

```ruby
Rails.application.config.assets.paths << Rails.root.join('app', 'assets', 'paperscripts')
```

additionally add `application.paper.js` to precompiled assets in the same file (`config/initializers/assets.rb`)

```ruby
Rails.application.config.assets.precompile += %w( application.paper.js )
```

create the file `app/assets/paperscripts/application.paper.js` and set it up to include all files in it's directory

```js
//= require_tree .
```

finally in your main `application.html.erb` add a `javascript_include_tag` for it:

```erb
    <%= javascript_include_tag('application.paper', type: "text/paperscript", canvas: "canvas-1") %>
```

note that with multiple paperscripts intended for more than one canvas you will either have to include
them separately or manage PaperScope/canvas binding from javascript/paperscript. 

## Contributing

Bug reports and pull requests are welcome on GitHub at https://github.com/[USERNAME]/paperjs.
