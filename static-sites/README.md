# Tutorial: Integrate With Your Static Site
In this tutorial you will learn how to embed query results from UseSQL into your static site. This will be very similar to the methods used in the Ghost tutorial. If anything is unclear feel free to reach out for assistance.

## Step 1: Build Your Query In Sandbox or OpenAPI Docs
You have a couple of options to streamline the creation of your queries. The one we will use in this tutorial will be using your standbox. We will be submitting the following query to the sandbox to generate our API request.
```sql
SELECT a.Symbol, a.Security, b.Executive 
FROM "https://en.wikipedia.org/wiki/List_of_S%26P_500_companies" a 
JOIN "https://raw.githubusercontent.com/dylanroy/ceo-dataset/main/data.csv" b ON a.Security = b.Company
```
Which generates the following request
```
https://usesql.com/sql?query=SELECT%20a.Symbol%2C%20a.Security%2C%20b.Executive%20%0AFROM%20%22https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FList_of_S%2526P_500_companies%22%20a%20%0AJOIN%20%22https%3A%2F%2Fraw.githubusercontent.com%2Fdylanroy%2Fceo-dataset%2Fmain%2Fdata.csv%22%20b%20ON%20a.Security%20%3D%20b.Company&format=html&key={YOUR_API_KEY}
```

Note: You can try this out for yourself if you are logged in [here](https://www.usesql.com/demo?query=SELECT%20a.Symbol%2C%20a.Security%2C%20b.Executive%20%0AFROM%20%22https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FList_of_S%2526P_500_companies%22%20a%20%0AJOIN%20%22https%3A%2F%2Fraw.githubusercontent.com%2Fdylanroy%2Fceo-dataset%2Fmain%2Fdata.csv%22%20b%20ON%20a.Security%20%3D%20b.Company). If you don't have an account you can also use the demo interface [here](https://www.usesql.com/sandbox?query=SELECT%20a.Symbol%2C%20a.Security%2C%20b.Executive%20%0AFROM%20%22https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FList_of_S%2526P_500_companies%22%20a%20%0AJOIN%20%22https%3A%2F%2Fraw.githubusercontent.com%2Fdylanroy%2Fceo-dataset%2Fmain%2Fdata.csv%22%20b%20ON%20a.Security%20%3D%20b.Company).

## Step 2: Embed Your Query
```html
  <div id="sql-result"></div>
  <script>
  fetch('https://usesql.com/sql?query=SELECT%20a.Symbol%2C%20a.Security%2C%20b.Executive%20%0AFROM%20%22https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FList_of_S%2526P_500_companies%22%20a%20%0AJOIN%20%22https%3A%2F%2Fraw.githubusercontent.com%2Fdylanroy%2Fceo-dataset%2Fmain%2Fdata.csv%22%20b%20ON%20a.Security%20%3D%20b.Company&format=html&key={YOUR_API_KEY}')
  .then(response => response.text())
  .then(data => document.getElementById('sql-result').innerHTML = data);
  </script>
  ```
At this point you can see your results. The demo can be seen [here](https://usesql.github.io/tutorials/static-sites/) with the styling from step 4, and the source can be seen [here](index.html).

## Step 3: Secure Your Key (Optional)

## Step 4: Style Your Table (Optional)
Embed in head.
```css
<style>
    #sql-result > table {
        border: 1px solid black;
        padding: 4px;
    }
    #sql-result > table tr td {
        border-top: 1px solid black;
    }
</style>
```

### Completed: Enjoy Your Results
[here](https://usesql.github.io/tutorials/static-sites/)