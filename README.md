# python-ile-cbs-final-odevi
final odevi kapsaminda   QGIS programi uzerinden python kodlamasiyla clip islemi gerceklestirilmistir.
Chatgpt yardimiyla visual studio code uzerinden nasil bir kodlama yapilmasi gerektigi soruldu.
chatgpt'nin verdigi kod su sekildeydi;
from qgis.core import QgsVectorLayer, QgsVectorFileWriter, QgsProcessingFeedback
from qgis.analysis import QgsNativeAlgorithms
from qgis import processing

Prepare the paths to your input and clip layers
input_layer_path = 'C:/Users/talat/OneDrive/Masaüstü/ARCGIS/İLÇE_SINIRI/İLÇE_SINIRI.shp'
clip_layer_path = 'C:/Users/talat/OneDrive/Masaüstü/ARCGIS/İLÇE_SINIRI/calisma_alani.shp'
output_layer_path = 'C:/Users/talat/OneDrive/Masaüstü/ARCGIS/İLÇE_SINIRI/outputclip.shp'

input_layer = QgsVectorLayer(input_layer_path, 'input_layer', 'ogr')
clip_layer = QgsVectorLayer(clip_layer_path, 'clip_layer', 'ogr')

if not input_layer.isValid() or not clip_layer.isValid():
    print('Invalid layers. Please check your file paths.')
    exit()

parameters = {
    'INPUT': input_layer,
    'OVERLAY': clip_layer,
    'OUTPUT': output_layer_path
}

feedback = QgsProcessingFeedback()
processing.run("native:clip", parameters, feedback=feedback)

clipped_layer = QgsVectorLayer(output_layer_path, 'clipped_layer', 'ogr')

if clipped_layer.isValid():
    print('Clipping process successful.')
else:
    print('Error during clipping process. Please check your input data and try again.')
    
Bu kod vsc ile yazildi. input, clip yapilacak dosya ve output yollari güncellendi.
input dosyasi ankara ilce siniri verisinden,
clip yapilacak dosya ise ayni verinin (ankara ilce siniri) QGIS uzerinden calisma alani adi altinda olusturdugum poligon katmani ve bu katmanin sayisallastirilmasindan olusmustur.
daha sonra vsc ile hazırlanan kod QGIS uzerinden calistirildi ve islem basariyla gerceklesti.
son olarak final odevi repositorysi visual studio code'a eklenerek calisma sonlandirildi.
