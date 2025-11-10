To enhance the performance of UI reports with 500k records, the primary
strategy is to avoid loading all the data into the browser's memory and
DOM simultaneously. The key is to manage data fetching and rendering
efficiently using the following frontend and backend techniques:

### Frontend Strategies

**Virtual Scrolling:** This is the most crucial technique
for large lists. It involves rendering only the items currently visible
in the user's viewport, plus a small buffer, and reusing DOM elements as
the user scrolls. Libraries like `react-window` or `react-virtualized`
can help implement this efficiently.

**Pagination:** Display a limited, fixed number of records per page
(e.g., 50-100) and provide navigation controls to fetch subsequent
pages. This reduces the initial load time and the number of DOM
elements.

**Infinite Scroll (Lazy Loading):** Similar to pagination, data is
loaded in chunks as the user scrolls toward the end of the current list.
This provides a smoother user experience than clicking "next page" but
requires careful implementation to prevent the DOM from becoming too
large over time.

**Data Summarization/Aggregation:** Instead of showing every single raw
record in an initial overview, display summary statistics or aggregated
tables. Users can then drill down into specific, smaller subsets of data
for details.

**Client-Side Caching:** Store frequently accessed but non-volatile data
(like user preferences or static report parameters) in browser storage
(e.g., `LocalStorage`, `IndexedDB`) to reduce repeated API calls.

### Smarter User Experience Design

-   Set reasonable default filters so the initial report load is small.\
-   Provide clear filtering and sorting options to help users narrow
    down the required data set before loading it.\
-   Use skeleton loaders or placeholders to improve the perceived
    performance while data is being fetched and rendered.
