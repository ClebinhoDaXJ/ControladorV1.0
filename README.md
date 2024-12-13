# ControladorV1.0
FirmwareV1.0.0

## Bibliotecas usadas
[SD](https://github.com/arduino-libraries/SD)
[arduino-LoRa](https://github.com/sandeepmistry/arduino-LoRa)
[TinyGPSPlus](https://github.com/mikalhart/TinyGPSPlus)
[Adafruit_BMP3XX](https://github.com/adafruit/Adafruit_BMP3XX)
[SparkFun_ICM-20948_ArduinoLibrary](https://github.com/sparkfun/SparkFun_ICM-20948_ArduinoLibrary)

## Cartão SD usado somente para guardar o vídeo de uma das câmeras.
O controlador V1.0 só possui 1 cartão SD, a princípio acho melhor usá-lo somente para guardar o vídeo
de uma das câmeras porque para guardar outros dados, como a altitude ou o vídeo da outra câmera, seria 
necessário ficar abrindo e fechando um monte de arquivos. 

## Módulo LoRa trasmite somente dados de altitude.
No começo é melhor testar a transmissão de uma pequena quantidade de dados. Até porque o módulo LoRa e o SDcard usam o mesmo barramento SPI, então quando um está  ativo o outro está inativo.

## Ciclos de amostragem e superciclo.
O IMU tem velocidade de amostragem bem maior que o BMP por exemplo, então se no código do loop a gente puser 'getIMU()' e em seguida um 'getBMP()' (essas funções são só um exemplo, significa que foram feitas amostragens dos sensores) a velocidade do IMU vai ser limitada pelo BMP. Então é melhor ter um ciclo de amostragens flexível em que possamos, por exemplo, pegar 6 amostras do IMU e em seguida, 1 amostra do BMP.

Configurar o ciclo de amostragem será possível por meio da função config_cicle(). Ao fim de cada ciclo ocorre o tratamento de dados e a sensorfusion por meio do filtro de Kalman.
