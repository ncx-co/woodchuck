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
