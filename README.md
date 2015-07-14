RubyMotionContributors
===================


Quick demo of RubyMotion

```
1. bundle
2. rake pod:install
3. rake
```

![screenshot](https://raw.githubusercontent.com/zhigang1992/RubyMotionContributors/master/screenshots/all.png)


```ruby
class HomeScreen < PM::TableScreen

  REQUEST_URL = 'https://api.github.com/repos/HipByte/RubyMotion/contributors'

  title "RubyMotion Contributors"
  refreshable
  searchable

  stylesheet HomeScreenStylesheet

  def on_load
    @contributors = []
    load_contributors
  end

  def table_data
    [{
        cells: @contributors.map do |c|
          {
            title: c[:login],
            subtitle: c[:url],
            action: :mp,
            arguments: {
              url: c[:url]
            }
          }
        end
      }]
  end

  def load_contributors
    AFMotion::JSON.get(REQUEST_URL) do |r|
      @contributors = r.object
      stop_refreshing
      update_table_data
    end
  end
  alias_method :on_refresh, :load_contributors
end
```

This is all the code to it.
