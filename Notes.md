
# Summary
- During my time on this project I was learning/working with Elixir & Phoenix on the fly and I was trying to relate the tech with my experience with JavaScript & React. When I was building inside the `regions_controller.ex` I was assuming if I created another function inside the `RegionController` that would `fetch_regions` it would allow `@region` & `@regions` to persist together inside the Socket state and allow me to iterate thorugh regions to be able to display the fetched data but `@regions` was rendering `undefined`. So then I started thinking that the fetch call to `fetch_regions` had to have it's own controller to be able to persist thorugh the Socket state and would also need its own `scope` inside the `router.ex`, as I was coding that part out I realized that this would have all the regions on its own page and the ReadMe stated that displaying all `Regions` needed to be on the same page as `nearest region`. After some time scanning through the documentation and elixir forum, the solution I came up with was to include another Case statement inside the `RegionController`'s `index` function that would allow the `fetch_regions` data to be assign to the connection and would allow both `@region` and `@regions` to persist together inside the Socket state. Then this allowed me to run a for loop inside `index.html.heex` which would allow me to key into each region and render every region's `name` & `code` from `fetch_region` API. After completing the fetch and meeting the requirments, I chagned the width of the nav bar to be 100% by removing it's` class=container ` since it was only rendering the width to 75%, by removing the ` class='container'` from the <main> tag this caused the child elements inside the html to shift all the way to the left side of the screen. I added an increase in margin-left: `ml-10` to give it more space from the left side of the screen's border. I also added padding-top: `pt-8` to give more spacing between the  `All Regions` H1 tag. If I had more time I would like to style the P tag's font-family and increase it's fonts weight and possibly adding some more spacing in-between each region that is listed.




# Scratch notes that I took while

What is going on inside:
-api route query is coming from `region_controller.ex`
-data is added to the `index.html.heex` file :
-inside `region_controller` instead of Client.fetch_nearest_region change it to:
    Client.fetch_regions which should change the html to all regions

-Need to be able to access the `fetch_regions` tuple then be able to iterate through that data to be able to display in the HTML

Passing Data with Phoenix & HTML : https://www.phoenix-tutorial.com/read/Customizing-Your-First-Phoenix-Page/Passing-Data


- fech all regions api is working and pritning inside the termial
    - try and create a index.html page that takes in all the regions and iterates over them
    - incoming data is formatted as [ {}, {}, {}]


Plan :
    - have fetch request be able to render on its own html page
    - iterate through the data while rendring each key/value pair


// Your nearest region is <%= @region["name"] %> (<%= @region["code"] %>)

     <%= for item <- @regions do %>
          <p><%= item["name"] %> (<%= item["code"] %>)</p>
          <% end %>

-Need to figure out what is going on with controller
- figure out how to use multiple controllers

      case Client.fetch_regions(client_config(conn)) do
        {:ok, regions} ->
          # assign(socket, key, value)
          # controller defines the api fetch values as @region
          assign(conn, :regions, regions)

        {:error, :unauthorized} ->
          put_flash(conn, :error, "Not authenticated")

        {:error, reason} ->
          Logger.error("Failed to load apps. Reason: #{inspect(reason)}")

          put_flash(conn, :error, reason)
      end


Styling Notes
- on <main> tag removed class='container' : to allow for the nav bar's width to be 100%
    - but due to removing the tab the elements inside
- changed mx-auto to be ml-10 due to the change of postioning of the elements after the class='container' was removed from the <main> tag
