# Ciao Mondo!

Appunti per me stessa

250124
in terminal:

- created new conda env
  (base) lauraholyn@Dexters-Mac-mini ciao-mondo % conda create -n gdalpip python=3.11

# Name of new environment is gdalpip

and activate

> conda activate gdalpip

- within the new env set up, install osgeo (gdal) ...would work with usual pip install (boo), forced it with:
  (gdalpip) lauraholyn@Dexters-Mac-mini ciao-mondo % conda install -c conda-forge gdal
- and updated conda (as recommended in output)
  ==> WARNING: A newer version of conda exists. <==
  current version: 23.7.4
  latest version: 23.11.0

Please update conda by running
$ conda update -n base -c defaults conda

# location of env is: /Users/"lh"/anaconda3/envs/gdalpip

- Set up new jupyter notebook in vscode: view>command palette - then use search bar "Create jupyter notebook" easy peasy.
- Set kernal with new conda env (gdalpip)

# ran code snippets for imports, had issues with matplotlib.pyplot. In terminal and installed (pip install matplotlib) ...e' funziona.

# Va bene, pronta.

260124

# Linking to file path containing imagery and Open with gdal, also print dataset type (should be <class 'osgeo.gdal.Dataset'>)

fn = "C:/qgis/raster/img_name.tif"

d1 = gdal.Open(fn)
print('d1 type', type(d1))

# Look at the metadata of the raster

print("Projection", d1.GetProjection())
print("Columns (xsize)", d1.RasterXSize)
print("Rows (ysize)", d1.RasterYSize)
print("Bands", d1.RasterCount) # number of bands

# Look at the coordinate values (prints as tuple) for each corner of the image. output: top left X coord (long), X pixel E-W resolution (in degrees, or check UNIT on projection info), top Y coord (Lat), pixel height (top to bottom pixel res)

d1.GetGeoTransform()

# Look at raster data. output: # of rows and no. of columns - should match above output on raster size. Also check shape

data_array = d1.GetRasterBand(1).ReadAsArray()
data.array.shape

# Display at the raster, in color

plt.figure(figsize=(10,10))
plt.imshow(data_array)
plt.colorbar()

# No data values in raster (later)

# to close raster

d1 = None
