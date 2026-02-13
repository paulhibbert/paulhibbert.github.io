---
title: Work in Progress GitHub Pages Site
layout: default
permalink: /
---

## CV

[On Render](https://paulhibbert.onrender.com/)

## Articles & Code Snippets

Most of the code I have written over the last ten years is in private repositories and I find it actually upsetting that many of my best moments and potentially useful learnings are forever hidden from me. However I have cobbled together some snippets and observations of a generic nature and plan to update with whatever code I can write in the open where it strikes me as interesting or I want to show knowledge.

### Laravel

- [A simple feature flag package for Laravel](articles/features)
- [Simple FormRequest example](articles/accepted-if-rule)
- [Using the authorize method in FormRequest](articles/merging)
- [Extending a Spatie composer package](articles/activity-log)
- [Casting a JSON column as a DTO](articles/casting)
- [A missing string helper?](articles/concat)
- [DIY API versioning](articles/why-not)
- [Custom Validation Rule for Password](articles/validation)
- [More account activation validation](articles/activation)
- [More custom validation unique value in array](articles/unique-in-array)
- [Adding a custom card to Laravel Pulse](articles/pulse)
- [Overriding Pulse Slow requests Recorder](articles/slow)
- [How do we solve a problem like Maria](articles/without-overlapping)

### Vue

- [My journey with Vue](articles/my-journey-with-vue)
- [Alert, a single file Vue component](articles/alert)
- [Another component using Alert](articles/success)
- [Vue component with named slot](articles/modal-component)

### SQL

However convenient ORMs are, in the end its all SQL underneath, and I actually think SQL is my favourite language. I don't have many snippets available unfortunately. One absolutely essential feature of Laravel's database query interface that is also available for Eloquent is `->toRawSQl()`, sometimes you really need to see the compiled query to validate what's being sent to the database server, or take it as the basis for something more complex where the ORM obscures what the functionality is.

- [Rollup](articles/rollup)

## Repositories

[GitHub](https://github.com/paulhibbert?tab=repositories&q=&type=public)

## Interesting Laravel Changes

There are so many features added to the framework by the core team and the community that it is definitely hard to keep track. I always take a close look at each framework release, but I have not always made a note about the additions that strike me as interesting. Let's see if I can be more consistent in future.

### v12.51.0

- [whenFails and whenPasses for Validator](laravel/validator)

### v12.50.0

- [Unique Queued Listeners](laravel/queued-listeners)
- [HasMany method for Collections](laravel/has-many-collections)
- [Clamp added to InteractsWithData trait](laravel/request-clamp)
