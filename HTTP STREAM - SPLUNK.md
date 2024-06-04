
# HTTP STREAM - SPLUNK


To analyze the HTTP stream between two specific IP addresses in Splunk, regardless of whether these IP addresses are the source or destination, you can create a search query that captures all relevant HTTP events. This involves searching for events where either IP address is present in either the source or destination fields and then filtering for HTTP traffic.

Here’s how you can construct the search query:

1. **Identify the Index and Sourcetype**: Assume `index=your_index` and `sourcetype=http_logs` (replace these with your actual index and sourcetype).

2. **Specify the IP Addresses**: Assume the two IP addresses are `192.168.1.1` and `10.0.0.2`.

3. **Search for Relevant Events**: Capture events where either IP address appears in either the source or destination fields.

4. **Filter for HTTP Traffic**: Ensure you are looking specifically at HTTP events.

### Example Search Query

```spl
index=your_index sourcetype=http_logs 
(source_ip="192.168.1.1" OR dest_ip="192.168.1.1" OR source_ip="10.0.0.2" OR dest_ip="10.0.0.2") 
| table _time, source_ip, dest_ip, http_method, uri, status, bytes_in, bytes_out, user_agent
| sort _time
```

### Explanation

1. **index=your_index sourcetype=http_logs**:
   - Searches within the specified index and sourcetype for HTTP logs.

2. **(source_ip="192.168.1.1" OR dest_ip="192.168.1.1" OR source_ip="10.0.0.2" OR dest_ip="10.0.0.2")**:
   - Filters events to include only those where either `192.168.1.1` or `10.0.0.2` is present in either the `source_ip` or `dest_ip` fields.

3. **| table _time, source_ip, dest_ip, http_method, uri, status, bytes_in, bytes_out, user_agent**:
   - Formats the output into a table with relevant fields: timestamp (`_time`), source IP (`source_ip`), destination IP (`dest_ip`), HTTP method (`http_method`), requested URI (`uri`), HTTP status code (`status`), bytes received (`bytes_in`), bytes sent (`bytes_out`), and user agent (`user_agent`).

4. **| sort _time**:
   - Sorts the results by the timestamp to show the communication in chronological order.

### Customizing for Your Environment

- **Index and Sourcetype**: Ensure you replace `index=your_index` and `sourcetype=http_logs` with the actual index and sourcetype used in your Splunk environment.
- **IP Addresses**: Replace `192.168.1.1` and `10.0.0.2` with the actual IP addresses you are investigating.
- **Additional Fields**: You can add or remove fields in the `table` command based on the specific details you need for your analysis.

### Advanced Example with Field Extraction

If your logs have different field names or require field extraction, you might need to adjust the query accordingly. For instance, if HTTP events are logged under different field names, use the appropriate field names in your search:

```spl
index=your_index sourcetype=http_logs 
((src_ip="192.168.1.1" OR dest_ip="192.168.1.1") OR (src_ip="10.0.0.2" OR dest_ip="10.0.0.2")) 
| eval source_ip=coalesce(src_ip, source_ip), dest_ip=coalesce(dest_ip, destination_ip)
| table _time, source_ip, dest_ip, http_method, uri, http_status, bytes_in, bytes_out, user_agent
| sort _time
```

### Explanation

1. **((src_ip="192.168.1.1" OR dest_ip="192.168.1.1") OR (src_ip="10.0.0.2" OR dest_ip="10.0.0.2"))**:
   - This ensures that events are captured regardless of the specific field names used (`src_ip` or `dest_ip`).

2. **| eval source_ip=coalesce(src_ip, source_ip), dest_ip=coalesce(dest_ip, destination_ip)**:
   - The `eval` command with `coalesce` helps to standardize the field names, making sure `source_ip` and `dest_ip` are consistently named for further processing.

Using this query structure, you can effectively analyze the communication between the two IP addresses from the beginning, ensuring all relevant HTTP traffic is captured and presented in a clear, chronological format.