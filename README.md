
### Manage Your Taggable Model

The API is intutive and very straightfarwad, so let's give it a quick look:

```php
// Instantiate your model
$post = new \App\Models\Post();

// Attach model tags
$post->attachTags(1); // attach single existing tag ID
$post->attachTags([1, 2, 5]); // attach multiple existing tag IDs array
$post->attachTags(collect([1, 2, 5])); // attach multiple existing tag IDs collection
$post->attachTags(app('rinvex.taggable.tag')->first()); // attach single tag model instance
$post->attachTags('A very new tag'); // attach single new/existing tag name created/retrieved & attached automatically
$post->attachTags(['First Tag', 'Second Tag']); // attach multiple new/existing tag names array created/retrieved & attached automatically
$post->attachTags(collect(['First Tag', 'Second Tag'])); // attach multiple new/existing tag names collection created/retrieved & attached automatically
$post->attachTags(app('rinvex.taggable.tag')->whereIn('id', [1, 2, 5])->get()); // attach multiple existing model instances

// Detach model tags
$post->detachTags(); // detach all tags
$post->detachTags(1); // detach single existing tag ID
$post->detachTags([1, 2, 5]); // detach multiple existing tag IDs array
$post->detachTags(collect([1, 2, 5])); // detach multiple existing tag IDs collection
$post->detachTags(app('rinvex.taggable.tag')->first()); // detach single tag model instance
$post->detachTags('A very new tag'); // detach single existing tag name
$post->detachTags(['First Tag', 'Second Tag']); // detach multiple existing tag names array
$post->detachTags(collect(['First Tag', 'Second Tag'])); // detach multiple existing tag names collection
$post->detachTags(app('rinvex.taggable.tag')->whereIn('id', [1, 2, 5])->get()); // detach multiple existing model instances

// Get attached tags collection
$post->tags;

// Get attached tags query builder
$post->tags();

// Check model has any of the given tags
$post->hasTag(['my-new-tag', 'my-brand-new-tag']);

// Check model has all of the given tags
$post->hasAllTags(['my-new-tag', 'my-brand-new-tag']);
```

> **Notes:** 
> - The `attachTags()` method attach the given tags to the model without touching the currently attached tags, while there's the `syncTags()` method that can detach any records that's not in the given items, this method takes a second optional boolean parameter that's set detaching flag to `true` or `false`.
> - You may have multiple tags with the same name and the same locale, in such case the first record found is used by default. This is intended by design to ensure a consistent behavior across all functionality whether you are attaching, detaching, or scoping model tags.
