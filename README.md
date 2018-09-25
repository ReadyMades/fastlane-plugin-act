# act plugin

[![fastlane Plugin Badge](https://rawcdn.githack.com/fastlane/fastlane/master/fastlane/assets/plugin-badge.svg)](https://rubygems.org/gems/fastlane-plugin-act) [![Build Status](https://travis-ci.org/richardszalay/fastlane-plugin-act.svg?branch=master)](https://travis-ci.org/richardszalay/fastlane-plugin-act)

## Getting Started

This project is a [fastlane](https://github.com/fastlane/fastlane) plugin. To get started with `fastlane-plugin-act`, add it to your project by running:

```bash
fastlane add_plugin act
```

## About act

Applies changes to plists, files, and app icons inside an xcarchive bundle or compiled IPA, making it easy to build once and release multiple times with different configurations 🎭

## Example

Check out the [example `Fastfile`](fastlane/Fastfile) to see how to use this plugin. Try it by cloning the repo, running `fastlane install_plugins` and `bundle exec fastlane test`. 

Here's some usage scenarios:

```ruby
# Modify the application Info.plist
act(
  archive_path: "example/Example.xcarchive",

  iconset: "example/Blue.appiconset",

  # Set a hash of plist values
  plist_values: {
    ":CustomApplicationKey" => "Replaced!"
  },

  # Run a list of PlistBuddy commands
  plist_commands: [
    "Delete :DebugApplicationKey"
  ]
)

# Modify a different application plist
act(
  archive_path: "example/Example.xcarchive",

  # Using a relative path indicates a plist file inside the .app
  plist_file: "GoogleService-Info.plist",
  
  plist_values: {
    ":TRACKING_ID" => "UA-22222222-22"
  }
)

# Modify the xcarchive manifest plist
act(
  archive_path: "example/Example.xcarchive",
  
  # Prefixing with a / allows you to target any plist in the archive
  plist_file: "/Info.plist",
  
  plist_values: {
    ":TRACKING_ID" => "UA-22222222-22"
  }
)

# Modify Info.plist in an IPA
act(
  archive_path: "example/Example.ipa",

  iconset: "example/Blue.appiconset",

  # Set a hash of plist values
  plist_values: {
    ":CustomApplicationKey" => "Replaced!"
  },

  # Run a list of PlistBuddy commands
  plist_commands: [
    "Delete :DebugApplicationKey"
  ]
)

# Replace a file with a local one (files only - asset catalog items are not supported)
act(
  archive_path: "example/Example.ipa",

  replace_files: {
    "GoogleService-Info.plist" => "example/New-GoogleService-Info.plist"
  }
)

# Remove a file (files only - asset catalog items are not supported)
act(
  archive_path: "example/Example.ipa",

  remove_files: [
    "GoogleService-Info.plist"
  ]
)
```

## Run tests for this plugin

To run both the tests, and code style validation, run

```
rake
```

To automatically fix many of the styling issues, use 
```
rubocop -a
```

## Issues and Feedback

For any other issues and feedback about this plugin, please submit it to this repository.

## Troubleshooting

If you have trouble using plugins, check out the [Plugins Troubleshooting](https://github.com/fastlane/fastlane/blob/master/fastlane/docs/PluginsTroubleshooting.md) doc in the main `fastlane` repo.

## Using `fastlane` Plugins

For more information about how the `fastlane` plugin system works, check out the [Plugins documentation](https://github.com/fastlane/fastlane/blob/master/fastlane/docs/Plugins.md).

## About `fastlane`

`fastlane` is the easiest way to automate building and releasing your iOS and Android apps. To learn more, check out [fastlane.tools](https://fastlane.tools).
