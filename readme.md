## EVERFI: You probably should not use this fork of globalize-versioning!

This repo is a fork of [a fork](https://github.com/TerraCycle/globalize-versioning/) which made the original/canonical [globalize-versioning](https://github.com/globalize/globalize-versioning/) gem Rails 5 compatible. This repo was moot once [globalize-versioning](https://github.com/globalize/globalize-versioning/) 0.3.0 was released, but we didn't realize it and kept using our fork of a fork.

These are the globalize/globalize-versioning versions you can use depending on your app's Rails version:

* **Rails 5.x**: globalize-versioning >= 0.3.0
* **Rails 6.x**: globalize-versioning >= 0.4.0

# Globalize Versioning 

## Introduction

`globalize-versioning` provides an interface between globalize and versioning gems such as
[PaperTrail](https://github.com/airblade/paper_trail).

At the moment, only `paper_trail` is supported, but support for other versioning gems is
planned for the future. Pull requests are always welcome.

## Installation

````ruby
gem install globalize-versioning
````

When using bundler, add this line to your `Gemfile`:

```ruby
gem 'globalize-versioning'
```

## Usage

To add versioning
support to your model, just add the `:versioning` option to your
call to <code>translates</code> with the name of the versioning gem as its value.
For example:

```ruby
translates :title, :content, :published, :published_at, :versioning => :paper_trail
```

You will also need to have already generated the versions table that `paper_trail`
expects.  See the paper_trail README for more details.

To pass options to the versioning gem, replace the gem name with a hash, and include
the options as the value of the `:options` key:

```ruby
translates :title, :content, :published, :published_at, :versioning => { :gem => :paper_trail, :options => { :on => [ :update ] } }
```

To access versions of a translated model, use the format: `post.translation.versions`.
Earlier versions of the globalize versioning support delegated `version` and `versions`
to the model translation (so you could access them with just `post.versions`), but
this causes problems if versioning is used on non-translated attributes, and has thus been removed.

## Adding globalize versioning to previously versioned models

If you are adding globalize to any previously versioned models, please note
that you will need to add a new `locale` column to your versioning table.

## Other gotchas

Please see the tests in `test/globalize-versioning/` for more details.

## License

See [LICENSE](LICENSE) for details.
