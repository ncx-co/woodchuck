# Cruise Data

CruiseData is just a JSON object that contains data that has the fields
specified in a Protocol.  The only sneaky bit is that it's a big nested object,
so it will look like:

```
# cruise level
{
	stand-name: 'demo stand',
	protocol: {    # all the protocol info
		'merch_specs': {...},
        'cruise': {...},
		'plot': {...},
		'tree': {...},
		'segment': {...},
		'subplot': {...},
		'subplot_tree': {...},
		'subplot_segment': {...}
    },
    merch_specs: {
        'name': " ",
        'id': “ ”,
        'merchandize_topwood': “ ”,
        'region': “ “,
        'uploader': “ “,
        rules: [
            {
            'name': <name>,
            'volume_unit': “ “,
            'minimum_diameter_outside_bark_inches': “ “,
            'maximum_diameter_outside_bark_inches': “ “,
            'minimum_top_diameter_outside_bark_inches': “ “.
            'minimum_log_length_feet': “ “,
            'product_group': “ ”,
            'stumpage_value': “ “,
            'pref_log_length': “ “,
            'length_cut_buffer_inches': “ “,
            'stump_height_feet': “ “,
            'buck_to_nearest_feet': “ “,
            'species': “ “,
            'species_common': “ “,
            'catch_all': “ “,
            'maximum_allowable_defect_percentage': “ “,
            'require_full_butt_log': “ “,
            'require_explicit_product_call': “ “,
            'description': “ “,
            'priority': “ “
            }
        ]
	...
	plots: [
		# plot level
		{
			'number': 1,
            'trees': [
	            # tree level
	            ...
            ] 
        },
        ...
    ]
}
```
