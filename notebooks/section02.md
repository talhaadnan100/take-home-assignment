# Section 2: Quantifying Similarity between Items

### Time Taken 59 Minutes

**Answer 1**: Due to practicality, the first indicator of similarity has to be based on `Size`. Then, the key distinguisher would be `Type` and this information is perhaps captured in greater detail in `Category ID`. Lastly, using other information such as `Vendor`. `Color` and `Keyword ID` to rank different similar items.

Reason being, a customer is typically spending their time browsing a web store in the search of a particular type or category of items. In regards to the three items mentioned, the items that seem most suitable to one another are `A`-`C`. Both these products are `M`-sized, `Top` and share 4 Category IDs as opposed to `B` which is a `L`-sized, `Bottom` with fewer matching Category IDs.

**Answer 2**: To efficiently scale calculating similarity, the inventory should first be filtered for similar `Size` and `Type` of products. This initial step will eliminate the most obviously dissimilar items. Then, sorting on number of matching `Category ID` in descending order. For same number of matching Category IDs, look for matching `Vendor` and `Color`. Lastly, match `Keyword ID`.

**Answer 3**: Although many data structures are suitable for this task, I would prefer a `data frame` because each product can be it's own row, and Keyword and Category IDs can be binarized. Hence the dimensions of the data frame would be 1105 columns (product ID, Type, Vendor, Color, Size, 100 Category IDs, 1000 Keyword IDs) and 100k rows for each product. The pseudo-code for the solution is:

```
# Let's look for the most similar products to our 1st product
product_0 = dataframe[[0]]

# Narrow down the data frame to possible similar candidates
similar_candidates = dataframe.filter(Type == product_0['Type'] & Size == product_0['Size'])

# Build a score column into the results based on match
# Initially, the score is the sum of Category IDs match
similar_candidates['Score'] = sum(product_0[5:105] == similar_candidates[5:105])

# Then add to it other similarities to differentiate between same scores
# Color and Vendor add a 10th of the score for match and each Keyword ID match adds 100th of a score
similar_candidates['Score'] += (product_0['Color'] == similar_candidates['Color'] +
                                product_0['Vendor'] == similar_candidates['Vendor]) * 0.01 +
                                sum(product_0[106:] == similar_candidates[106:]) * .001

# Lastly, sort data frame based on score column
similar_candidates.sort('Score', descending = True)
```
