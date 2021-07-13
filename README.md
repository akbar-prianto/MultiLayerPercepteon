MultilayerPerceptronJS


MultiLayer Perceptron

Lihat posting blog saya .

Ini adalah "perpustakaan" jaringan saraf kecil yang ditujukan untuk tujuan pendidikan. Saya ingin mengembangkan sesuatu yang mudah dipahami dan sangat mudah dibaca, sehingga perpustakaan ini jauh dari optimal atau efisien.

Menginstal
Anda dapat menginstal ini melalui npm

npm instal multilayer-perceptron-js
Membuat jaringan saraf
const  { MultiLayerPerceptron , ActivationFunction }  =  membutuhkan ( 'multilayer-perceptron-js' ) ;

biarkan  sigmoid  =  new  ActivationFunction ( 
  x  =>  1  /  ( 1  +  Math . exp ( - x ) ) ,  // sigmoid 
  y  =>  y  *  ( 1  -  y )  // turunan dari sigmoid 
) ;

biarkan  mlp  =  new  MultiLayerPerceptron ( { inputDimension : 2 } ) 
  . addLayer ( { node : 2 ,  aktivasi : sigmoid } ) 
  . addLayer ( { node : 2 ,  aktivasi : sigmoid } ) 
  . addLayer ( { node : 1 ,  aktivasi : sigmoid } ) 
  .randomizeWeights ( ) ;
Melatih jaringan saraf
mlp . kereta ( { 
  trainData : dataset . masukan , 
  trainLabels : dataset . target , 
  validationData : validationDataset . masukan , 
  validationLabels : validationDataset . target , 
  numEpochs : numberOfEpochs , 
  learningRate : learningRate , 
  verbose : benar 
} ) ;
Dimana dataset.inputs, dataset.targets, validationDataset.inputs, dan validationDataset.targetsadalah array. Jika Anda memecahkan masalah XOR, datasetmungkin terlihat seperti ini (sehingga indeks setiap array berbaris):

biarkan  kumpulan data  =  { 
  input : [ 
    [ 0 ,  0 ] , 
    [ 0 ,  1 ] , 
    [ 1 ,  0 ] , 
    [ 1 ,  1 ] 
  ] , 
  target : [ 
    [ 0 ] , 
    [ 1 ] , 
    [ 1 ] , 
    [ 0 ] 
  ] 
} ;
Anda akan melihat sesuatu seperti ini saat berlatih jika verbose adalah true:

Zaman 10 ; Kesalahan 1.9860974914165456
...
Zaman 100 ; Kesalahan 0.76609707552872275
...
Zaman 1000 ; Kesalahan 0.166096867598113085
...
Zaman 5000 ; Kesalahan 0,036096035894226
...
Zaman 10.000 ; Kesalahan 0,03609582796927307
...
Membuat prediksi
Untuk membuat prediksi, sebut saja predictpada MultiLayerPerceptronobjek. Anda akan menerima tebakan yang diprediksi dan status jaringan saraf. Jika Anda memiliki model yang memecahkan masalah XOR, membuat prediksi akan terlihat seperti ini:

konsol . log ( mlp . prediksi ( [ 0 ,  0 ] ) . prediksi ) ;  // [0.02039202706589195] 
konsol . log ( mlp . prediksi ( [ 0 ,  1 ] ) . prediksi ) ;  // [0.9848467111547554] 
konsol . log ( MLP . memprediksi ( [ 1 ,  0 ] ) .prediksi ) ;  // [0.9850631024542238] 
konsol . log ( mlp . prediksi ( [ 1 ,  1 ] ) . prediksi ) ;  // [0.013544196415469074]
Ucapan Terima Kasih
Sebagian besar implementasi terinspirasi dari video The Coding Train di jaringan saraf, dan video 3Blue1Brown di jaringan saraf membantu saya memahami apa yang saya lakukan jauh lebih baik.
