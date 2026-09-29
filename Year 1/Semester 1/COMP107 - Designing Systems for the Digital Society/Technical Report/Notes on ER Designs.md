## Categories of User
Our app doesn't contain super neat distinct categories like staff and student so to separate the categories into different views we've had to be creative.
#### The key points here from my understanding was this:
- Each view is meant to represent the knowledge needed by the different parts of the app that people can interact with.
- They aren't meant to contradict each other.

#### The 3 categories, as I understood it, were
- Eco Friendly Homebody - Only focused on the shopping and smart meter parts of our app, completely ignores travel and cares about both price and environmental impact.
- Frequent Traveller - Only focused on the travel part of our app, does not care about shopping or household impact but cares about minimising the price and environmental impact of their journeys.
- Budget Focused - Uses every part of our app but only cares about the price and cost information. Everything only relevant to environmental impact is ignored.

## Kevin
### User
Price Priority doesn't need to be an attribute here since Kevin is only using the app to minimise his costs anyway. Price priority is the sort of attribute that we should use to differentiate the Kevins from the Susans. So therefore Kevin's view doesn't need it.

User can search for journeys, vendors, products and product types. Since the system would need that data to recommend things to the user.

There could be multiple users in the same household and some people may have multiple houses and therefore multiple smart meters.

### Vendor 
I added a type attribute to separate different kinds of vendors.

Vendor, the entity, is individual shops and stores, not chains. So location doesn't need to be a multivalued attribute since different Tescos would have different entries and IDs although they may share Names and Cost Scores.

Multiple vendors can offer the same products and do not have to offer any products so it is a non-mandatory many to many relationship.
### Products & Product Types
Products are contained within product type. They must be part of a type but have their own unique IDs and are therefore not weak entities identified through their product type. This allows for reclassifying products into different product types if a more appropriate one is identified.
### Journey
Many journeys can be travelled by many Users.

Journeys must contain at least 1 route, but the same route could appear in many different journeys (For example he same flight appearing in 2 users journeys who have with different routes to or from the airport) so therefore it is both a mandatory and many to many relationship.

The Total Distance, Total Cost, and Total Time are derived from the distances, costs and times of the contained routes, and would not need to be stored in the database but would be useful for our users.

### Route
Route can be both a specific train journey, bus journey, or flight (etc) or it can be a path that would be travelled by driving, cycling, walking etc.

Routes must always have an associated transport method, and the cost and time would be affected by changing this so Route must be a weak entity identified by the "Travelled With" with relation. This could be subject to change.

 Cost is not a derived attributes in the case of Route as some Transport Methods, such as flights, busses and trains, will have set prices, although for cars it would be derived from the cars attributes and the distance of the route itself but then stored afterwards.
### Transport Method
Transport methods would be both specific cars, planes, busses, cabs, and trains OR cycling or walking.

Cycling and walking would obviously given the speed of the average cyclist or pedestrian for their speed attribute, a Fuel Type of Null, a Fuel Consumption and Fuel Cost Value of 0, and a Type value of "Cycling" or "Walking". Having the null value is acceptable since cycling and walking are special cases and null would not commonly be stored.

For planes, cars and busses (and etc) their "Type" would be one of "Plane", "Car", "Bus" and then the other attributes would be determined by the specific vehicle.

The fuel information is necessary for determining cost of transport when driving yourself.

I have done away with it being a class and the different methods of transport being their own entities since it felt redundant. Having one transport method class with the Type attribute and the attributes said are enough.

Similarly I have done away with transport providers entirely since if you know the kind of vehicle, cost of route etc, there isn't much reason for  the system to know about specific transport providers.

### Smart Meter and Smart Meter Report
One User could have multiple homes and therefore link multiple smart meters. Similarly one smart meter could be linked by multiple users living in the same home. This means the Links relationship is a many to many relationship between smart meters and users.

The information on a smart meter is a bit too complicated to be stored in a column of a table and so we would need to store reports from the smart meter over time. This means that Smart Meter Report is a weak entity identified by the its owner and the date and then the costs for each utility would be stored there for a specific interval of time. Probably a month.

## Homebody

### Issues
- The travel section of the graph isn't necessary since this is the view for the homebody.
- Redundancy from shopping item and food and drink. They have exactly the same attributes and therefore there isn't really any meaningful difference that would require them to be separate entities. Replacing both with product seems like it would be better. The "Product Type" Entity also doesn't exist in this diagram.
- Multiple vendors can sell the same product so having products be a weak entity doesn't fit.
- There doesn't seem to be any reference to environmental impact of entities within their attributes.
- The searches for relationship isn't present.
- Cardinality of relationships isn't present aside from a few Ns.

