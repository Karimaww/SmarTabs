#include <Servo.h>
#include <SPI.h>
#include <MFRC522.h> // библиотека "RFID".
#define SS_PIN 10
#define RST_PIN 9
MFRC522 mfrc522(SS_PIN, RST_PIN);
unsigned long uidDec, uidDecTemp;  // для храниения номера метки в десятичном формате
Servo yazik;
Servo vorota;
Servo kriwka;
boolean flag = true;
boolean flag1 = true;
void setup() {
  Serial.begin(9600);
  Serial.println("Waiting for card...");
  SPI.begin();  //  инициализация SPI / Init SPI bus.
  mfrc522.PCD_Init();     // инициализация MFRC522 / Init MFRC522 card.
  yazik.attach(6);
  vorota.attach(5);
  kriwka.attach(3);
  yazik.write(175);  // устанавливаем серву в закрытое сосотояние
  vorota.write(180);
  kriwka.write(180);
}
void loop() {
  // Поиск новой метки
  if ( ! mfrc522.PICC_IsNewCardPresent()) {
    return;
  }
  // Выбор метки
  if ( ! mfrc522.PICC_ReadCardSerial()) {
    return;
  }
  uidDec = 0;
  // Выдача серийного номера метки.
  for (byte i = 0; i < mfrc522.uid.size; i++)
  {
    uidDecTemp = mfrc522.uid.uidByte[i];
    uidDec = uidDec * 256 + uidDecTemp;
  }
  Serial.println("Card UID: ");
  Serial.println(uidDec); // Выводим UID метки в консоль.
  if (uidDec == 3763176269&&flag) // Сравниваем Uid метки, если он равен заданому то серва открывает.
  {
    vorota.write(0);
    delay(2000);
    yazik.write(100);
    flag=false;
  }
  
   else if (uidDec == 3763176269&&!flag)
  {
    vorota.write(180);
    delay(2000);
    yazik.write(175);
    flag=true;
    }

      if (uidDec == 1922520097&&flag1) // Сравниваем Uid метки, если он равен заданому то серва открывает.
  {
    kriwka.write(90);
    flag1=false;
  }
  
   else if (uidDec == 1922520097&&!flag1)
  {
    kriwka.write(180);
    flag1=true;
    }
   
    delay(4000);

  
 // servo.write(0);  // устанавливаем серву в закрытое сосотояние
}
