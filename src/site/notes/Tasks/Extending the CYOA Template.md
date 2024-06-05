---
{"dg-publish":true,"permalink":"/tasks/extending-the-cyoa-template/","dgHomeLink":true,"dgShowToc":true}
---

# Extending the CYOA Template

## Purpose

The Choose Your Own Adventure Template has been provided as an example of how to implement and use a [directed graph](https://www.russellgordon.ca/lcs/2023-24/ics4u/joyce-judy.pdf) to tell a story with many possible endings.

![RocketSim_Screenshot_iPhone_15_6.1_2024-06-05_07.02.48.png|700](/img/user/Media/RocketSim_Screenshot_iPhone_15_6.1_2024-06-05_07.02.48.png)

## Next steps

Now that your group member(s) have completed authoring their part of the story, it is your group's job to demonstrate that each group member knows how to use [[Concepts/Source Control Within a Team\|source control within a group]] and that you can collaborate effectively to improve a product. 

> [!IMPORTANT]
> Be certain you have read and understand the [evaluation criteria for the culminating task](https://drive.google.com/file/d/1OHXEhbi5CYiBmtdE4ryaPH981yRjSV2-/view?usp=share_link).
> 
> **Not being aware of the evaluation criteria is not valid reason for not meeting these criteria by the end of the module.** Your grade on this task will represent what *you* personally have contributed to the success of your group's effort:
> 
> ![Screenshot 2024-06-05 at 7.46.18 AM.png](/img/user/Media/Screenshot%202024-06-05%20at%207.46.18%E2%80%AFAM.png)

## Exemplars

Here are some examples of how the CYOA Template was extended last year by prior Grade 12 Computer Science students:

![RocketSim_Screenshot_iPhone_15_6.1_2024-06-05_07.02.48 1.png|700](/img/user/Media/RocketSim_Screenshot_iPhone_15_6.1_2024-06-05_07.02.48%201.png)

These students built a story where the reader is immersed in an epic *"Will she / won't she?"* love triangle drama.

![RocketSim_Screenshot_iPhone_15_6.1_2024-06-05_07.02.48 2.png|700](/img/user/Media/RocketSim_Screenshot_iPhone_15_6.1_2024-06-05_07.02.48%202.png)

The story of aspiring rap star, Kendrick – notable enhancements here include a graph of the story outline that updates as the reader moves through the story, to show what paths have been travelled.

![RocketSim_Screenshot_iPhone_15_6.1_2024-06-05_07.02.48 3.png|700](/img/user/Media/RocketSim_Screenshot_iPhone_15_6.1_2024-06-05_07.02.48%203.png)

These students extended the template into a game of sorts, where various criteria (energy, food levels) change based on what parts of the story are visited. This provides the player with a sense of whether they have chosen a helpful or unhelpful path.

## Database schema

Here are some tips about the database schema you have been provided with.

![Screenshot 2024-06-05 at 7.32.24 AM.png](/img/user/Media/Screenshot%202024-06-05%20at%207.32.24%E2%80%AFAM.png)

The `page` table holds each page (node) of the directed graph. When `ending_context` and `ending_type_id`  are filled in, the page is marked and categorized as an ending when [generating the directed graph](https://www.russellgordon.ca/lcs/2023-24/ics4u/directed-graph-example.png) using the `GraphGenerator` app.

The `ending_type` table lists the five possible ending types:

![Screenshot 2024-06-05 at 7.36.18 AM.png|350](/img/user/Media/Screenshot%202024-06-05%20at%207.36.18%E2%80%AFAM.png)

The `edge` table connects each page (node) to possible pages that the reader can move to next.

The `reader` table is designed to hold preferences and state for a given user of the game. For example, the **Journey Under the Sea** exemplar story has been read by several people over the past few days, and the contents of the `reader` table track what page each user last read in their current trip through the story:

![Screenshot 2024-06-05 at 7.38.00 AM.png](/img/user/Media/Screenshot%202024-06-05%20at%207.38.00%E2%80%AFAM.png)

Settings (such as whether dark mode was enabled) are also tracked and stored. This table could be extended by your group to include additional preferences, if you choose to add those to your app.

Finally, the `reader` table is designed to track what pages a given reader has visited and read. For example, this entry in the `reader` table shows that a reader – reader `17` – had visited and read page `1`:

![Screenshot 2024-06-05 at 7.40.57 AM.png](/img/user/Media/Screenshot%202024-06-05%20at%207.40.57%E2%80%AFAM.png)

As that same reader visits more pages, additional rows would need to be added. The `reader_id` value would always be `17` for that user, and the `user_id` value would also be identical. Only the `page_id` would differ for each new row – the `page_id` value tracks what page number has been read.

> [!NOTE]
> 
> The CYOA Template does not actually populate this table – but that is an enhancement that your group could add so that your app keeps track of what pages a given user has read.
> 
> The `user_id` is automatically populated by Supabase when a row is added to this table. Mr. Gordon will speak to what this value represents in class.

## Final advice

Have fun with this culminating task! Assume best intentions of your group members. Be patient and when in doubt – communicate. Remember to [[Concepts/Source Control Within a Team\|follow these steps]] when using source control.