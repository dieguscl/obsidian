- **Measurement** is the name given to a set of data points that represent the same kind of metric recorded over time. Think of it as the subject of the data you are collecting. For example, if you are recording temperature data, the measurement might be 'temperature'. It's a way to categorize the data for easy retrieval and association. Usually it is analogous to a table.

- **Fields** are the individual data points associated with a measurement. They contain the actual values being recorded. Each field has a name and a value. For instance, if your measurement is 'temperature', a field could be 'average_temperature' with a numeric value representing the average temperature at a given time.

- **Labels** or **Tags** provide context to the measurements. They are additional descriptors or identifiers that do not change as frequently as field values. Labels could be static attributes like location (e.g., 'server_room'), device ID, or any other metadata that helps in filtering and querying the data without being the data itself.

Aliases are used to categorize each column

- `m:` prefix for a measurement name.
- `t:` prefix for a timestamp.
- `f:` prefix for a field.
- `l:` prefix for a label or tag.