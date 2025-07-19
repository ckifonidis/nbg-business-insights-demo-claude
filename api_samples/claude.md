# API Samples Claude Guide

## Overview
This directory contains sample API requests and responses for the NBG Business Insights dashboard. All API calls target the `/analytics/query` endpoint.

## Sample Files Structure

### Analytics Samples
- `analytics/request.json` - Full dashboard request with all metric IDs
- `analytics/response.json` - Complete response with merchant + competitor data
- `analytics/request_with_filters.json` - Request with filter parameters
- `analytics/response_with_filters.json` - Filtered response data

### Revenue Samples  
- `revenue/revenue_metrics_request.json` - Basic revenue metrics request
- `revenue/revenue_metrics_response.json` - Revenue metrics response
- `revenue/revenue_goformore_metrics_request.json` - Go 4 More specific request
- `revenue/revenue_goformore_metrics_response.json` - Go 4 More response
- `revenue/revenue_breakdown_interests_request.json` - Interest breakdown request
- `revenue/revenue_breakdown_interests_response.json` - Interest breakdown response
- `revenue/revenue_by_channel_request.json` - Channel breakdown request
- `revenue/revenue_by_channel_response.json` - Channel breakdown response

## Key API Patterns

### Request Structure
```json
{
  "header": { "ID": "{{$guid}}", "application": "..." },
  "payload": {
    "userID": "...",
    "startDate": "YYYY-MM-DD", 
    "endDate": "YYYY-MM-DD",
    "metricIDs": ["metric1", "metric2"],
    "filterValues": [...],
    "metricParameters": {...}
  }
}
```

### Response Structure
```json
{
  "payload": {
    "metrics": [
      {
        "metricID": "...",
        "percentageValue": boolean,
        "scalarValue": "number_as_string" | null,
        "seriesValues": [...] | null,
        "merchantId": "merchant_name" | "competition"
      }
    ]
  }
}
```

## Metric ID Mapping
See root `instructions.md` section "Metric to Metric ID mapping" for complete mapping between UI metrics and API metric IDs.

## Filter Usage
- `interest_type=revenue` - For revenue-based breakdowns
- `data_origin=own_data` - Standard filter for merchant data
- Age, gender, channel filters available per UI requirements

## Data Types
- **Scalar**: Single values in `scalarValue` field
- **Time Series**: Daily data points in `seriesValues` with date/value pairs
- **Category Breakdown**: Category data in `seriesValues` with category/value pairs

## Merchant vs Competition
- Responses include both merchant and competitor data
- Identified by `merchantId` field: merchant name vs "competition"
- Used for comparison metrics in UI components

## Metric Compatibility
**All metrics can be requested together in a single API call without conflicts.**

- The sample requests show different combinations for demonstration purposes
- In practice, you can combine any metric IDs in the `metricIDs` array
- Example: A single request can include scalar metrics, time series, and breakdown metrics
- The API will return all requested metrics in the same response structure
- This allows efficient data fetching for entire tabs with one API call

**Example combined request:**
```json
{
  "metricIDs": [
    "total_revenue",           // Scalar metric
    "revenue_per_day",         // Time series metric  
    "converted_customers_by_gender", // Category breakdown
    "avg_ticket_per_user"      // Another scalar metric
  ]
}
```
All metrics will be returned in the `metrics` array, each with their appropriate data structure.