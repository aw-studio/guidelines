# Vue

## Filtering

<p>Filtering will be handled with Vue and A small Laravel API.</p>

### Filter Frontend

<p>The frontend of the filter will be handled entirely by Vue.<br/>
First an Array of Values for the filter should be passed to a vue component via a prop. this array should be looped over using a v-for loop and then there should be a function add(filteritem), which adds the selected item to a new array <strong>selected</strong>.<br/>
In the next step there should be a function submit(), which does an API call via axios to a post route that is given by laravel. This submit can be called either when a seperate button is pressed or each time the add function is called.</p>

```javascript
async submit() {
    const { data } = await axios.post("/api/events", {
        category_ids: _.map(this.selected, category => {
            return category.id;
        }),
    });
    this.events = data;
}
```

### Filter Backend

<p>The backend of the filter is handled within Laravel as an API route.<br/>
In the routes api file a post route should be created which calls a function int the pageController. There the function should be called post<em>NameOfTheModel</em> (e.g. postEvents).<br/>
The function has a request with the selected items from the frontend as its parameter and then runs a query on the model that should be filtered.</p>

```php
public function postEvents(Request $request)
    {
        $category_ids = $request->category_ids;

        if (collect($category_ids)->isNotEmpty()) {
            $events = Event::whereHas('categories', function ($query) use ($category_ids) {
                $query->whereIn('category_id', $category_ids);
            })->get();
        } else {
            $events = Event::all();
        }
        return $events;
    }
```

<p>If there are no items selected in the frontend the post route should simply return all values of the model</p>
