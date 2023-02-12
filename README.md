# A Cesium Vue Test Project

### Install Dependencies
`yarn install`

### Start project in dev enviroment
`yarn dev`

### Build Project
`yarn build`


## This is a Coding Challenge by the following description

A website should be created showing a 3D Map on the right side and an information section on the
left side.\
3D Map:\
Technology: CesiumJS -- https://cesium.com/learn/cesiumjs-learn/ \
The map should show the following datasets:
- Berlin buildings: Tileset:\
  https://www.virtualcitymap.de/datasource-data/f892f6af-180a-4eef-917f-5ff03c260b32/tileset.json 
- Germany terrain: CesiumTerrainProvider:\
  https://www.virtualcitymap.de/datasource-data/globalterrain_5_9 
  
Both datasets can be used with Cesiumjs.

Information section:\
- Technology: VueJS\
- The information section should show object related information. On a click at a 3d
object/building in the 3D Map the attributes of the building should be shown.
  - To do this its
  required to listen to a click event in the CesiumJS 3D Map.\
  In the Berlin buildings dataset, the data to be shown is encoded in the “attributes” Attribute.
- Further Requirements:
- Git should be used.
- The Project should be an NPM Package, inclusive buildtools to build the webpage.

To submit:\
The code should be hosted on a free git hosting application or can be provided as a zip file
which includes the git repository.