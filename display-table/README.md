### Displays a formatted table based on structured json  

The prompt gives display and formatting instructions. While the table displayed 
it tried to include HTML and failed to color the rows.
```
A plugin that gives the user stock data. Make sure to display in tabular format.
Bold the headers and color even and odd rows differently. If the market cap is
below 1 trillion then make the text font red.
```
<img width="877" alt="stocks-format" src="https://github.com/sisbell/chatgpt-plugins/assets/64116/cf23438a-c296-42c2-81c3-7f4c28564901">

The following prompt also has similar mistakes. Notice how ChatGPT inferred that you
also want the market cap above 1T in green, even though this is not given in the prompt.
```
A plugin that gives the user stock data. Make sure to display in tabular format.
Bold the headers. If a stock_id is odd color the row light blue.
If the stock_id is even, color the row light yellow. If the market cap is
below 1 trillion then make the market_cap text red.
```
<img width="857" alt="stocks-format2" src="https://github.com/sisbell/chatgpt-plugins/assets/64116/af66ea20-75e5-4a0f-bec2-79045d0f500c">