We will create a react vite application with typescript that has a UI that dsiplays tranasction and revenue infromation for a merchant and also in comparison with their competition.

# UI Design

## Basic Layout
The UI will be responsive and mobile first.

Sample of the initial page is under html_samples.
From this you must understand the basic look and feel of the UI.

The navigation is based on tabs. Each tab refer to a specific section of metrcis that we want to display.
The tabs will be displayed horizontally for desktop and as a dropdown for mobile.

They will ll be located between the tab content and the header.

The stable components are the header and the footer and a sidebar with filters on the left.
The sidebar on the left should be hidable both for mobile and desktop.

The tabs will be:
Dashboard
Revenue
Use a meaningful icon to display with each tab title.

The user lands initially on the Dashboard tab.
The user can navigate to the other tabs by clicking on them.
Each tab will be accessible by visiting home_url/tab_name

Each tab will have a title and a description.

The filter bar for the mobile version will be fullscreen, toggled by a button at the bottom right (floating, absolute position)

## Available Metric types

Each metric will have a title and a description.

There are 6 types of metric components: single, single metric full, row single metric with competition comparison, time series metric, bar chart and category breakdown metric.

When a behavior is determined by the metric displayed, this should mean that it is not decided/selectable by the user.
Instead, it is a configuration of the metric.

Metric components are meant to be re-usable components that are used by the actual metric implementations.

### Single Metric With Competition Comparison
Occupies full row.
For single metric 4 values will be displayed:
Merchant Value, Merchant Value Percentage difference vs Last Year.
Competition Value, Competition Value Percentage difference vs Last Year.
On the left side the merchant values, on the right side competition values.
Main focus on the value, secondary focus on the percentage difference vs last year.
Use icons that match the metric description.
Use icons that match the trend (increase/decrease).
Total of 3 icons must be used: Description, Merchant Trend, Competitor Trend.


### Single Metric
Occupies half or 1/3 row.
Shows only merchant value and percentage difference vs last year.
Rest behavior is the same as for Single Metric With Competition Comparison.

### Single Metrics Full Row
Occupies full row.
Can contain up to 3 Single Metric components.
Has its own title.

### Time Series Metric
Occupies full row.
For time series metric the date will be displayed in the x axis and the value in the y axis.
For the x axis, daily weekly and monthly aggreagation will be available.
Depending on the metric, the time series can either display a value or a percentage in the y axis.
It can display merchant data only, or merchant data and competition data for comparison.
The agreggation for value will be sum of the distinct values for the period, for percentage it will be average of the distinct values for the period.
All Time Series metrics support three view modes: line chart, bar chart and table (defined at component level).
Has tooltip: Hovering over a datapoinnt, the value of thfe merchant and competitor (if enabled) will be displayed, and also the percentage difference vs last year.

### Bar chart
For the bar chart, the y axis will display the value of the metric or the percentage it represents of the sum of a all categories and the x axis the category.
Value or percentage is decided based on the metric displayed.
The bar chart will display merchant and competitor data.
View mode will be either bar chart or table.
Has tooltip: Upon hovering on a bar, both actual value and percentage will be displayed.

### Category Breakdown Metric
Same as Bar Chart
All Category Breakdown metrics support three view modes: Pie chart, Table, Horizontal Stacked bar (defined at component level).

## Filters
Filter sidebar has each own store slice.
Filter changes should never trigger a data fetch.
The only way to fetch new data as a result of a filter change is when the user clicks on the Apply button.

Gender
Dropdown with Male/Female options

Age Groups
Dropdown with Generation Z, Millennials, Gen X, Boomers, Silent options

Channel
Dropdown with Physical stores/E-commerce options

Date Range
Date range picker with start and end date. (dd-mmy-yyyy format)


## Tab metrics

Each metric is of a specific type, requires specific data, it is connected with metric id and has specific display configuration

### Dashboard

#### Total Revenue
Type: Single Metric With Competition Comparison
Requires current and last year merchant data.
Requires current and last year competitor data.
Calculates revenue percentage difference vs last year.

#### Total Transactions
Type: Single Metric With Competition Comparison
Requires current and last year merchant data.
Requires current and last year competitor data.
Calculates transaction count percentage difference vs last year.

#### Average Transaction Value
Type: Single Metric With Competition Comparison
Requires current and last year merchant data.
Requires current and last year competitor data.
Calculates average transaction value percentage difference vs last year.

#### Daily Revenue
Type: Time Series Metric
Requires daily merchant data and last year daily merchant data for the period.
Requires daily competitor data and last year daily competitor for the period.
Y-axis displays revenue values.
Calculates daily revenue percentage difference vs last year.
Supports daily, weekly, and monthly aggregation (calculated client-side from daily data).

#### Daily Transactions
Type: Time Series Metric
Requires daily merchant data and last year daily merchant data for the period.
Requires daily competitor data and last year daily competitor for the period.
Y-axis displays transaction count values.
Calculates daily transaction count percentage difference vs last year.
Supports daily, weekly, and monthly aggregation (calculated client-side from daily data).

#### Daily Customers
Type: Time Series Metric
Merchant Data Only.
Requires daily merchant data and last year daily merchant data for the period.
Y-axis displays customer count values.
Calculates daily customer count percentage difference vs last year.
Supports daily, weekly, and monthly aggregation (calculated client-side from daily data).


### Revenue

#### Total Revenue
Type: Single Metric With Competition Comparison
Requires current and last year merchant data.
Requires current and last year competitor data.
Calculates revenue percentage difference vs last year.

#### Average Daily Revenue
Type: Single Metric With Competition Comparison
Requires current and last year merchant data.
Requires current and last year competitor data.
Calculates average daily revenue percentage difference vs last year.

#### Average Transaction Value
Type: Single Metric With Competition Comparison
Requires current and last year merchant data.
Requires current and last year competitor data.
Calculates average transaction value percentage difference vs last year.

#### Daily Revenue
Type: Time Series Metric
Requires daily merchant data and last year daily merchant data for the period.
Requires daily competitor data and last year daily competitor for the period.
Y-axis displays revenue values.
Calculates daily revenue percentage difference vs last year.
Supports daily, weekly, and monthly aggregation (calculated client-side from daily data).

#### Daily Revenue Trend Vs Last Year
Type: Time Series Metric
Requires daily merchant data and last year daily merchant data for the period.
Requires daily competitor data and last year daily competitor for the period.
Y-axis displays percentage difference vs last year.
Calculates daily revenue percentage difference vs last year.
Supports daily, weekly, and monthly aggregation (calculated client-side from daily data).

#### Revenue By Gender
Type: Category Breakdown Metric
Requires merchant data grouped by gender.
Requires competitor data grouped by gender.

#### Revenue By Interest
Type: Category Breakdown Metric
Requires merchant data grouped by interest.
Requires competitor data grouped by interest.

#### Go 4 More
Type: Single Metric Full Row
Contains 3 Single Metric components:
- Total Revenue Go 4 More
Requires current and last year merchant data.
Calculates value percentage difference vs last year.
- Total Rewards Go 4 More
Requires current and last year merchant data.
Calculates value percentage difference vs last year.
- Total Redeemed Go 4 More
Requires current and last year merchant data.
Calculates value percentage difference vs last year.


## Techincal

### Store

The store will be implemented using Redux Toolkit.
The store will contain the following slices:
- filters
- dashboard
- revenue
- ui

### Api Integration

Api request/respons samples can be found here: /api_samples

All data retrieval api requests target the same endpoint: /analytics/query

Each metric is mapped to specific Metric ID.

Depending of the metrics included in a tab, different Metric IDs will be requested.

Each tab performs a specific API request with the required metric IDs in order to populate the required metric implementation.

The request is performed twice, once for the current year and once for the last year, respecting always the date range filter.

### Metric to Metric ID mapping

#### Dashboard Tab
- Total Revenue → total_revenue (calculated from total_transactions * avg_ticket_per_user)
- Total Transactions → total_transactions  
- Average Transaction Value → avg_ticket_per_user
- Daily Revenue → revenue_per_day
- Daily Transactions → transactions_per_day
- Daily Customers → customers_per_day

#### Revenue Tab  
- Total Revenue → total_revenue
- Average Daily Revenue → avg_daily_revenue
- Average Transaction Value → avg_ticket_per_user
- Daily Revenue → revenue_per_day
- Daily Revenue Trend Vs Last Year → revenue_per_day (percentage mode)
- Revenue By Gender → converted_customers_by_gender (with filter: interest_type=revenue)
- Revenue By Interest → converted_customers_by_interest (with filter: interest_type=revenue)
- Go 4 More (Single Metric Full Row containing):
  - Total Revenue Go 4 More → goformore_amount
  - Total Rewards Go 4 More → rewarded_amount  
  - Total Redeemed Go 4 More → redeemed_amount


### Data Flow

When a tab is selected, the following happens:
- The tab is rendered
- The tab performs an API request for the required metrics
- The API response is mapped to the required metric format
- The metric data is stored in the store
- The metric components are rendered
- The metric components display the data from the store

Unti the data requested by a tab is available, the tab will display a loading state.

No caching, deduplication or any other sort of optimization will be implemented.
The goal is to maintain the cleanest architecture possible without any additional complexity.

### Components

Layout component: Header, Footer, Filter Side bar, Tab Content
Tab Content: List of Metric Rows
Metric Row: List of Metric Component Implementations e.g. <TotalRevenue>

The Metric Component implementation (aka Bespoke Component) provides connection to the store to pass to the Metric Component the required data and specific configuration for the metric being displayed.

Metric Components should remain as simple as possible, and should not contain any business logic.

## Tools

You can you use  Browser-tools MCP Server to:
Read console and network logs.
Take screeshots. Screenshots will be located ~/Downloads/mcp-screenshots
This can help you debug.

## Development

We will start implementation with the Dashboard tab.
We will not integrate the API immediately.
Instead, the bespoke components will create and pass mock data to the metric components.
When we need to debug, you will ask me to visit the page you want to debug.
You add logs beforehand and you read the console and network logs from the browser-tools MCP Server.

### TypeScript Note

- `verbatimModuleSyntax` is enabled. Ensure import/export syntax is compatible.

### Project Setup Instructions

- You will provide scaffolding and bootstrapping commands (e.g. for project creation, library installation, and folder structure).
- These commands will be executed manually by the user.
- Consult tool Context 7 for library information