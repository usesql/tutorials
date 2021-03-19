# Tutorial: Integrate With Your Static Site
In this tutorial you will learn how to embed query results from UseSQL into your static site. This will be very similar to the methods used in the Ghost tutorial. If anything is unclear feel free to reach out for assistance.

## Step 1: Build Your Query In Sandbox or OpenAPI Docs
You have a couple of options to streamline the creation of your queries. The one we will use in this tutorial will be using your standbox. We will be submitting the following query to the [sandbox](https://www.usesql.com/sandbox) to generate our API request.
```sql
SELECT a.Symbol, a.Security, b.Executive 
FROM "https://en.wikipedia.org/wiki/List_of_S%26P_500_companies" a 
JOIN "https://raw.githubusercontent.com/dylanroy/ceo-dataset/main/data.csv" b ON a.Security = b.Company
```
Which generates the following request
```
https://usesql.com/sql?query=SELECT%20a.Symbol%2C%20a.Security%2C%20b.Executive%20%0AFROM%20%22https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FList_of_S%2526P_500_companies%22%20a%20%0AJOIN%20%22https%3A%2F%2Fraw.githubusercontent.com%2Fdylanroy%2Fceo-dataset%2Fmain%2Fdata.csv%22%20b%20ON%20a.Security%20%3D%20b.Company&format=html&key={YOUR_API_KEY}
```

Note: You can try this out for yourself if you are logged in [here](https://www.usesql.com/sandbox?query=SELECT%20a.Symbol%2C%20a.Security%2C%20b.Executive%20%0AFROM%20%22https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FList_of_S%2526P_500_companies%22%20a%20%0AJOIN%20%22https%3A%2F%2Fraw.githubusercontent.com%2Fdylanroy%2Fceo-dataset%2Fmain%2Fdata.csv%22%20b%20ON%20a.Security%20%3D%20b.Company). If you don't have an account you can also use the demo interface [here](https://www.usesql.com/demo?query=SELECT%20a.Symbol%2C%20a.Security%2C%20b.Executive%20%0AFROM%20%22https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FList_of_S%2526P_500_companies%22%20a%20%0AJOIN%20%22https%3A%2F%2Fraw.githubusercontent.com%2Fdylanroy%2Fceo-dataset%2Fmain%2Fdata.csv%22%20b%20ON%20a.Security%20%3D%20b.Company).

After this you just need to either add a new key or use an existing key.
![](https://usesql.github.io/tutorials/docs/images/add-or-use-key.png)

## Step 2: Embed Your Query
```html
  <div id="sql-result"></div>
  <script>
  fetch('https://usesql.com/sql?query=SELECT%20a.Symbol%2C%20a.Security%2C%20b.Executive%20%0AFROM%20%22https%3A%2F%2Fen.wikipedia.org%2Fwiki%2FList_of_S%2526P_500_companies%22%20a%20%0AJOIN%20%22https%3A%2F%2Fraw.githubusercontent.com%2Fdylanroy%2Fceo-dataset%2Fmain%2Fdata.csv%22%20b%20ON%20a.Security%20%3D%20b.Company&format=html&key={YOUR_API_KEY}')
  .then(response => response.text())
  .then(data => document.getElementById('sql-result').innerHTML = data);
  </script>
  ```
At this point you can see your results. The demo can be seen [here](https://usesql.github.io/tutorials/static-sites/) with the styling from step 4, and the source can be seen <a href="https://github.com/usesql/tutorials/blob/main/static-sites/index.html#L17-L22" target="_blank">here</a>.

## Step 3: Secure Your Key (Optional)
It's pretty easy to secure our key. To add these restrictions we need to login, and navigate to our dashboard clicking on the domains link for the key that we want to add the restriction to shown below.
![](https://usesql.github.io/tutorials/docs/images/restrict-domains-1.png)

After that the domain for the static site needs to be entered. For the purposes of the tutorial the domain in this example is entered below. To add more than one domain you just need to seperate it by a comma.
![](https://usesql.github.io/tutorials/docs/images/restrict-domains-2.png)

## Step 4: Style Your Table (Optional)
The table is returned without any styling applied so in order to apply additional styles we just need to embed the styles applying them using the id we applied earlier to our sql-result. Take a look at the static site source to see how we applied the style below <a href="https://github.com/usesql/tutorials/blob/main/static-sites/index.html#L6-L14" target="_blank">here</a>.
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

## Completed: Enjoy Your Results
At this point you can take a look at the static site example we built through this tutorial [here](https://usesql.github.io/tutorials/static-sites/), and its source <a href="https://github.com/usesql/tutorials/blob/main/static-sites/index.html" target="_blank">here</a>.