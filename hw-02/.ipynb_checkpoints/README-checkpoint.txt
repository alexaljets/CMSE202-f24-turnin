
********************************** CREDITS **********************************

                         VERSION 1.11 - DECEMBER 2014

This README file accompanies the dataset representing the The Multilayer Temporal Network of Public Transport in Great Britain, produced by Riccardo Gallotti of the QuantURB group (http://www.quanturb.com). This work has been supported by European Commision FET-Proactive project PLEXMATH (Grant No. 317614) (http://www.plexmath.eu) and conducted under the supervision of Marc Barthelemy.

Please contact us (contact details can be found on www.quanturb.com) if you have any doubt, find errors or inconsistencies in the datasets, have suggestions or collaborations to propose.

******************************** DESCRIPTION ********************************

The dataset describes the Public Transport Network of Great Britain by use of a Multilayer node-list and edge-list, where each layer is associated to a mode of transport. Each node is geo-referenced, thus defining a spatial network, and associated to a wide list of administrative meta-data. 
For each edge, the minimal travel-time in minutes is indicated. For the case of inter-layer edges, this is defined as the walking time needed for the inter-modal connection. For each intra-layer edge, we also specify a list of temporal events representing the vehicles' rides along the edges, with origin time and travel duration expressed in minutes with a precision of one minute. 
In Multilayer networks, each node may have several 'copies' in different layers. For that reason, nodes are identified by two numbers, one specifying the node itself, and another the layer where it belongs. As a consequence, the edges are identified by four numbers, two for the origin and two for the destination (node and layer). The ordering of the fields in edge-list has been chosen to conform to the tensorial notation widely used for this kind of networks.
There is no established standard format for the temporal event list. Therefore, we decided to use a format, derived from the idea of adjacency lists, which has been specifically adapted to this dataset.

********************************** CONTENTS **********************************

All files are plain ASCII text files. Each row represents a record and, for all files but events.txt, has the same number of fields in the same order. Conversely, a non-standard format has been used for encoding the events information (see below).

-------------------------------------------------------------------------------

layers.csv

In this network, each layer represents a mode of transport.

layer: numerical id for each layer;
layerLabel: mode of transport associated to the layer.
-------------------------------------------------------------------------------

nodes.csv

The same node, identified by the same nodeid, may exist in different layers and is in this file represented once for each layer where it appears.

nodeid: numerical id for each node 
layerid: layer when the node appears;
lat: latitude;
lon: longitude;
areacode: using this code one may link node with the administrative areas information contained in "Admin Areas.csv" (where this key is called "ATCOcode") and then to "Travel Region.csv" through the "Traveline Region ID" key;
atcocode: the ATCOcode of a stop Area (Group) if its 4th character is 'G', or of a stop Point (Stop) if is '0'. With this code one may link nodes to the metadata of "Stops.csv" and "Groups.csv".
-------------------------------------------------------------------------------

edges.csv

Edges are directed and weighted. They can be either intra-layer, between different nodes in the same layer, or inter-layer, between the same node in different layers. We associate a weight to each edge which is given by the minimal travel time from the origin to the destination, in minutes. Edges are listed following the layers' hierarchy. The bus events are by far the most numerous (more than 90% of the total). The reading can be interrupted at the first edge belonging to this layer whenever the bus information is not needed.

ori_node: origin node;
des_node: destination node;
ori_layer: origin layer;
des_layer: destination layer;
minutes: minimal travel time between origin and destination in minutes;
km: the euclidean distance between origin and destination in kilometres.

-------------------------------------------------------------------------------

events.txt

The format for this file is the following:
ori_node,des_node,ori_layer,des_layer,t_1,dt_1,t_2,dt_2,...,t_n,dt_n

Here we use the comma as delimiter, and for each line of text, the first 4 elements represent the edge. The subsequent fields are a list of events. Each edge has a different number of events, and therefore each line a different number of fields. An event i is identified by two values, t_i and dt_i, and represents a ride starting at time t_i and of duration dt_i. Both times are in minutes. t_i is defined as minutes starting from the 00:00 of Monday.



************************ NaPTAN AND NPTG METADATA *****************************

We include the original files from the National Public Transport Access Node (NaPTAN) and National Public Transport Gazeetteer (NPTG). We encourage the reader to refer to the comprehensive guide "naptanschemaguide-2.5-v0.67.pdf", available online at the NaPTAN scheme webpage:

http://www.naptan.org.uk/schema/schemas.htm
(Download link: http://81.17.70.199/naptan/schema/2.5/doc/NaPTANSchemaGuide-2.5-v0.67.pdf ) 


Here the list of fields for each of these files:
-------------------------------------------------------------------------------
Stops.csv

ATCOCode
GridType
Easting
Northing
Lon
Lat
CommonName
Identifier
Direction
Street
Landmark
NatGazID
NatGazLocality
ParentLocality
GrandParentLocality
Town
Suburb
StopType
BusStopType
BusRegistrationStatus
RecordStatus
Notes
LocalityCentre
SMSNumber
LastChanged

-------------------------------------------------------------------------------
Groups.csv

GroupID
GroupName
Type
GridType
Easting
Northing
Lon
Lat
LastChanged

-------------------------------------------------------------------------------
Admin Areas.csv

Admin Area ID
Admin Area Name
Traveline Region ID
Country
ATCO Code
Call Centre ID
Date of Issue
Issue Version

-------------------------------------------------------------------------------
Travel Region.csv

Traveline Region ID
Region Name
Primary URL
Secondary URL
Tertiary URL
Date of Issue
Issue Version
JW Version

************************ INNOVATA TIMETABLES *****************************

To ensure the reproducibility of our dataset, we include the original timetable as provided by Innovata LLC.

-------------------------------------------------------------------------------
UKDOMESTICOCT10.csv

Mktg Al
Op Al
Orig
Dest
Kilometers
Flight
Stops
Equip
Seats
Dep Term
Arr Term
Dep Time
Arr Time
Block Mins
Arr Flag
Op Days
Ops/Week
Seats/Week

