---
layout: posts
---

Once I built out my custom dashboard using Google Sheets (read [my blog post on this topic](https://junhopark.com/posts/2017/02/17/building-a-custom-dashboard-using-google-sheets-and-sheetsu)) I decided that I wanted to look at the data for only the last 30 days.  While it's important that I have historical data dating back to when I initially put the dashboard together, on most days, I wanted to see quick snapshots of various trends for only the last 30 days.

Initially I set up a filter in Google Sheets (Top menu > Data > Filter) and my filtering was set on the date column to include only the last month's data.  The annoying issue with this approach, though, was that the filtering did not auto-adjust itself as days went by.  So, if on 2/1 I was looking at filtered records for the past 30 days, on 2/2 I was looking at the past 31 days and if I didn't refresh the filter every so often, before I knew it I was looking at way more data than just the past 30 days.

I was convinced that there has got to be a better way and I eventually came across a solution that works.  The solution entails using the "filter" formula and the wonderful thing about this approach is that my filtering auto adjusts itself!

Let's say that you have 2 columns of data in your Google Sheet document, like this:

<style type="text/css">
table {
    margin-bottom: 10px;
}

th, td {
    text-align: center;
}

td {
    padding: 5px;
}

.header {
    background-color: #193441;
    color: #fcfff5;
}

.system-cell {
    background-color: lightgray;
}
</style>

<table border="1">
    <tr>
        <th class="system-cell"></th>
        <th class="system-cell">A</th>
        <th class="system-cell">B</th>
    </tr>
    <tr>
        <td class="system-cell">1</td>
        <td class="header">Date</td>
        <td class="header"># of Errors</td>
    </tr>
    <tr>
        <td class="system-cell">2</td>
        <td>2/1/2017</td>
        <td>26</td>
    </tr>
    <tr>
        <td class="system-cell">3</td>
        <td>2/2/2017</td>
        <td>31</td>
    </tr>
    <tr>
        <td class="system-cell">4</td>
        <td>2/3/2017</td>
        <td>15</td>
    </tr>
    <tr>
        <td class="system-cell">5</td>
        <td>...</td>
        <td>...</td>
    </tr>
</table>

Leave Columns A & B untouched since these columns are meant to store all of your historical data.  Designate Column C as the filtered data for Column A & Column D as the filtered data for Column B, like this:

<table border="1">
    <tr>
        <th class="system-cell"></th>
        <th class="system-cell">A</th>
        <th class="system-cell">B</th>
        <th class="system-cell">C</th>
        <th class="system-cell">D</th>
    </tr>
    <tr>
        <td class="system-cell">1</th>
        <td class="header">Date</td>
        <td class="header"># of Errors</td>
        <td class="header">Date - Filtered</td>
        <td class="header"># of Errors - Filtered</td>
    </tr>
    <tr>
        <td class="system-cell">2</th>
        <td>2/1/2017</td>
        <td>26</td>
        <td></td><td></td>
    </tr>
    <tr>
        <td class="system-cell">3</th>
        <td>2/2/2017</td>
        <td>31</td>
        <td></td><td></td>
    </tr>
    <tr>
        <td class="system-cell">4</th>
        <td>2/3/2017</td>
        <td>15</td>
        <td></td><td></td>
    </tr>
    <tr>
        <td class="system-cell">5</th>
        <td>...</td>
        <td>...</td>
        <td></td><td></td>
    </tr>
</table>


Let's say you want Columns C & D to show data for only the last 30 days. You can use the following formula for Column C:

*=filter(A2:A, DAYS360(A2:A, TODAY()) < 30)*

and the following formula for Column D:

*=filter(B2:B, DAYS360(A2:A, TODAY()) < 30)*

If you don't care to look at the unfiltered data in Columns A & B, you can simply hide these columns by right-clicking on the column headers and selecting "Hide columns ...".

See the following Google Doc I've put together for an example of this:

[https://docs.google.com/spreadsheets/d/1R9q_Ldp_UuMvNs6o9E2KN95B0xa6ApXoTg3sM3eKCZw/edit#gid=0](https://docs.google.com/spreadsheets/d/1R9q_Ldp_UuMvNs6o9E2KN95B0xa6ApXoTg3sM3eKCZw/edit#gid=0)
