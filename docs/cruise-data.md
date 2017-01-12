# Cruise Data

CruiseData is just a JSON object that contains data that has the fields
specified in a Protocol.  The only sneaky bit is that it's a big nested object,
so it will look like:

Merch specs are included in the cruise data.  If catch_all is true then species, 
and species common will be empty arrays.  Otherwise if catch_all is false, then 
species will be an array of silviaterra species ids and species_common will be an 
array of species common names.

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
            'minimum_diameter_outside_bark_inches': <min butt dia>,
            'maximum_diameter_outside_bark_inches': <max butt dia>,
            'minimum_top_diameter_outside_bark_inches': <min top dia>.
            'minimum_log_length_feet': <min log length>,
            'product_group': <product group>,
            'stumpage_value': <stumpage>,
            'pref_log_length': <preferred log length>,
            'length_cut_buffer_inches': <length cut buffer inches>,
            'stump_height_feet': <stump height>,
            'buck_to_nearest_feet': <buck to nearest feet>,
            'species': <array of species ids>,
            'species_common': <array of species common names>,
            'catch_all': <catch all True/False>,
            'maximum_allowable_defect_percentage': <max defect>,
            'require_full_butt_log': <require full log True/False>,
            'require_explicit_product_call': <require explicit call True/False>,
            'description': <description>,
            'priority': <priority>
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
