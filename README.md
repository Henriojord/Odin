# Odin
Automatic generation of new monsters for Ragnarok Online

Model's codes are available in models/

You can directly try the Python notebooks in your Google colaboratory to experiment the models by yourself.  

I also plan to provide Python scripts soon.

## Plain Auto-Encoder

#### Model's architecture & other hyper-parameters
![plain_autoencoder](img/plain_autoencoder/model.png)

Auto-encoder's architecture:
* Encoder: 3 downsampling blocks. Each block consists in a several [convolutional layer-> batch normalization -> ReLU activation]. Also, each block is followed by a max-pool operation that halves the spatial dimensions. The number of convolutional filters is doubled by convolutional layers that follows each max-pooling operation (starting with 64 filters in the first block). The last convolutional block's feature map is flatten and passed through a fully-connected layer of 128 neurons.
* Decoder: Processes the latent vector produced by the encoder, which is first reshaped to form a 3 dimensional tensor (batch dimension omitted). Then, the decoder is made of 3 upsampling blocks. Each block (except the first one) starts with a bilinear interpolation and is then followed by several [convolutional layer -> batch normalization -> ReLU activation]. The number of convolutional filters is halved by convolutional layers following each interpolation operation (starting from 256 filters in the first block).  

Other hyper-parameters:
* Loss function: Mean Squared Error (MSE)
* Optimizer: Adam
* Learning rate: Fixed to 0.001
* Mini-batch size: 32
* Number of training epochs: 2000

#### Example of images produced by a plain autoencoder

Interpolation between a Poring and a Metaling (left), Portaling(50% Poring/50% Metaling) (right) :

![poring metaling interpolation](img/plain_autoencoder/poring-metaling-interpolation.gif) ![portaling](img/plain_autoencoder/portaling.png)

Interpolation between a Poring and Ifrit (left), Porfrit(30% Poring/70% Ifrit) (right) :

![poring ifrit interpolation](img/plain_autoencoder/poring-ifrit-interpolation.gif) ![porfrit](img/plain_autoencoder/porfrit.png)

## More models soon...
