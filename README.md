## The task

Using just historical sale data, we'd like to be able to answer a few specific questions:

  * What's the average individual purchase rate of users across the site?
  * Is there a common tendency in individual purchasing rates over time?
  * Has that common tendency itself changed over time?

Imagine the raw historical sale data are stored in a schema that looks like this:

  * Each sale is represented by an individual row in a table called `sales`. Columns include `sale_id`, `sale_date`, `buyer_email_address`, `num_items`, and `total_usd`.
  * For the purposes of this exercise, you can assume that if someone makes multiple purchases, they use the same email address each time.

Work your magic:

  1. Describe the final form (or forms) of what you might produce from the raw sale data, and how it all would address the primary questions.
  2. Describe (in writing) each step of the algorithmic process by which you would transform the raw data into that final form. Though you should assume you are engineering your hypothetical routine in R or Python, at this point we are not so much interested in particularities of code as we are in the conceptual steps by which you would aggregate, manipulate, and generally structure the data as you go along. Where relevant, detail any important design decisions or judgment calls you make, or where having more information could help.
  3. Explain everything in #1 and #2 again (!), but this time much simpler: keep the whole thing to just a few sentences about the essence of what is going on.
  4. In what ways could the final data be misinterpreted? What are the benefits and limitations of thinking in terms of an "average purchase rate" in the first place?

---

## The solution

  1. Describe the final form (or forms) of what you might produce from the raw sale data, and how it all would address the primary questions.
  
      i. My preferred form for communication is R Markdown, and I believe it would be appropriate here. I would write a static report to be published/distributed, but R Markdown also allows for a document to be easily turned into a set of slides or an interactive Shiny document if a live presentation or interactive dashboard is more appropriate.
    
      ii. The resulting document would at least contain:
      
              a. The average purchase rate, defined as the number of transactions per member, for the entire time frame in question.
      
              b. A plot showing the purchase rate over time in smaller time increments. This would show the general direction that the purchasing rate was moving over time.
      
              c. An additional plot, perhaps a boxplot or a beeswarm, that would reveal changes in the distribution of purchasers. This could answer important questions, such as, "Are all users buying more, or are a few users buying enough to drive up the whole average?"
          
      iii. Other aspects that I would explore and include, if they were compelling, are:
  
              a. Other definitions of average purchase rate. Number of purchases per member is a quick look, but it would be helpful to see average number of items, or average dollars paid out per member over time. 
      
              b. There may be some "super-users," outliers who bring the average of the block up with exceptionally high transaction activity. It would be beneficial to see how these users change over time, and what the churn is like on this sub-block.
      
              c. Proportion of single-purchase members.
      
              d. A regression or other statistical model to formalize the relationship between purchase rate and time.
  
  2. Describe (in writing) each step of the algorithmic process by which you would transform the raw data into that final form. Though you should assume you are engineering your hypothetical routine in R or Python, at this point we are not so much interested in particularities of code as we are in the conceptual steps by which you would aggregate, manipulate, and generally structure the data as you go along. Where relevant, detail any important design decisions or judgment calls you make, or where having more information could help.
      
      i. Average purchase rate would be a simple count of unique sale IDs over count of unique member IDs (`buyer_email_address`). Alternate definitions from 1.iii.a. above would be sum of the number of items over unique members and sum of purchase price over unique members, respectively.
      
      ii. Creating the plot noted in 1.ii.b. would be a simple task of making those calculations while grouping by month or quarter of the sales date.
      
      iii. The plot(s) in 1.ii.c. would require little data wrangling ahead of time, since a boxplot and a beeswarm both do aggregation with the plotting step. One way I would aggregate before plotting would be choosing what time span to aggregate by (month, quarter, year). This would just depend on how many years back it would be relevant to show.
      
      iv. One design decision that would be really interesting with the plots is marking past business initiatives. Perhaps at the start of the summer, a new advertising campaign was launched. That could be noted on the plots so that it would be clear how sales had changed after that point.
      
  3. Explain everything in #1 and #2 again (!), but this time much simpler: keep the whole thing to just a few sentences about the essence of what is going on.
  
      i. The essence of this analysis is simple. First, I would make sure to answer the specific questions asked, detailing any assumptions made. Then I would explore the data further to see if there are other significant patterns worth showing. Finally I would add some engaging prose to give context and narrative around the data.
  
  4. In what ways could the final data be misinterpreted? What are the benefits and limitations of thinking in terms of an "average purchase rate" in the first place?
  
      i. One might assume that increasing purchase rate means increasing revenue for both Bandcamp and artists. This highlights additional information that would be helpful in this analysis: The revenue generated by a given purchase can vary by whether it's music or merch, as well as whether the artist is a Bandcamp Pro subscriber. So even if every measure of purchase rate is increasing, if it all happened to be purchases from Bandcamp Pro artists, revenue for the company wouldn't increase. 
