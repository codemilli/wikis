The release of Guard v1.1 introduces some changes to the API used for creating guards. These changes were the result of moving a portion of the internal code that was used inside Guard to detect changes in directories into a new gem called [Listen](https://github.com/guard/listen). 

Upgrading existing guard to Guard v1.1 is a simple process. This guide will walk you through the new changes in the API for creating guards and how to use them to upgrade existing guards. If you are only intrested in a pracitcal example of upgrading a guard, you can skip to the section about [upgrading exising guards](#upgrade-existing-guards).

<a name="#new-methods"></a>
## New methods for handling changes
The `run_on_change` and `run_on_deletion` methods which were used to handle changes in directories are considered deprecated. Their use is not recommended as they will be removed sometime in the future. 

Guard v1.1 provides developers with **four** new methods for handling changes:

- `run_on_additions`: This method will be called when files are added to the watched paths. Use this method when you need to run some code for new files only.

- `run_on_modifications`:  This method will be called when either the modification-time (`mtime`) or the content of a file is changed in the watched paths.

- `run_on_removals`: This method still does the same thing that `run_on_deletions` did, namely running some code when files are removed from the watched paths. Its name was changed to keep the API consistent.

- `run_on_changes`: This method can be used to DRY the other methods mentioned above. Shared code that needs to run on any change should be put inside it. It can also be the only method implemented if the developer wants to run the same thing on all changes. Please note that this method does not do the same thing `run_on_change` did before; it is called for all methods that are not implemented (including `run_on_removals`). When overriding any of the other `run_on_*` methods, make sure to call `super` inside the overridden method if you want this method to be called before running the overridden method.

<a name="upgrade-existing-guards"></a>
## Upgrading existing guards to the new API

Consider the following example implementation of a guard written for Guard before version 1.1:

```ruby
require 'guard'
require 'guard/guard'

module Guard
  class MyGuard < Guard

    # Implementation of the other methods...

    def run_on_change(paths)
        # Do something with the changed paths
    end

    def run_on_deletion(paths)
        # Do something with the deleted paths
    end

  end
end
```

Although Guard 1.1 gives developers more control over the type of changes they want to handle (read more about it in the [section above](#new-methods)), converting that guard to the new API of Guard v1.1 while retaining the same functionality could be done in the following way:

```ruby
require 'guard'
require 'guard/guard'

module Guard
  class MyGuard < Guard

    # Implementation of the other methods...

    def run_on_changes(paths)
        # Do something with the changed paths

        # Note: This method will be called from `run_on_additions` and `run_on_modifications`
        #       because they are not implemented.
    end

    def run_on_removals(paths)
        # Do something with the deleted paths

        # Note: `super` is not called here, so `run_on_changes` won't be called
        #        before running this method!
    end

  end
end
```

And you are done. Now your guard is ready for Guard v1.1!