#define THRESHOLD 300
#define S0 4
#define S1 7
#define S2 8
#define S3 12
#define sensorOut 2
#define LM1 6       // left motor
#define LM2 9       // left motor
#define ENA 5
#define RM1 10       // right motor
#define RM2 11       // right motor
#define ENB 3

//Output from the sensor:
int redFrequency = 0;
int greenFrequency = 0;
int blueFrequency = 0;

//Formatted color values:
int redColor = 0;
int greenColor = 0;
int blueColor = 0;

//Values used for calibration
int redMin;
int redMax;
int greenMin;
int greenMax;
int blueMin;
int blueMax;

int color = 0;//gae  budhal
int warna = 0;// gae mbalik
int iro = 0;// gae mbalik

void MoveForward(void);
void MoveRight(void);
void MoveLeft(void);
void MoveBack(void);
void MoveSRight(void);
void MoveSLeft(void);
void Stop (void);

bool firstLoop_R = true;//iki nggarakno mlaku pisan tok
bool secondLoop_R = true;
bool thirdLoop_R = true;
bool fourthLoop_R = true;

bool firstLoop_G = true;//iki nggarakno mlaku pisan tok
bool secondLoop_G = true;
bool thirdLoop_G = true;
bool fourthLoop_G = true;

bool firstLoop_B = true;//iki nggarakno mlaku pisan tok
bool secondLoop_B = true;
bool thirdLoop_B = true;
bool fourthLoop_B = true;

bool penentu_R = true;
bool penentu_B = true;
bool p_R = true;
bool p_G = true;
bool p_B = true;

//Sensors Pins
int Out1 = A0;
int Out2 = A1;
int Out3 = A2;
int Out4 = A3;
int Out5 = A4;
int Out6 = A5;

//Sensor values initialization
int Sensor1 = 0;
int Sensor2 = 0;
int Sensor3 = 0;
int Sensor4 = 0;
int Sensor5 = 0;
int Sensor6 = 0;


void setup() {
  //Declarations:
  analogWrite(ENA, 250);
  analogWrite(ENB, 250);

  pinMode(Out1, INPUT);
  pinMode(Out2, INPUT);
  pinMode(Out3, INPUT);
  pinMode(Out4, INPUT);
  pinMode(Out5, INPUT);
  pinMode(Out6, INPUT);

  pinMode(S0, OUTPUT);
  pinMode(S1, OUTPUT);
  pinMode(S2, OUTPUT);
  pinMode(S3, OUTPUT);
  pinMode(sensorOut, INPUT);
  // Set frequency scaling to 20%:
  digitalWrite(S0, HIGH);
  digitalWrite(S1, LOW);

  pinMode(LM1, OUTPUT);
  pinMode(LM2, OUTPUT);
  pinMode(RM1, OUTPUT);
  pinMode(RM2, OUTPUT);

  pinMode(ENA, OUTPUT);
  pinMode(ENB, OUTPUT);
  Serial.begin(9600);//begin serial communication
  calibrate();//calibrate sensor (look at serial monitor)
  readColor();//read sensor
  decideColor();//format color values
  delay(2000);
}
void(* resetFunc) (void) = 0; //declare reset function @ address 0

void loop() {
  switch (color) {
    case 1: Serial.println("WHITE");
    while(1)
    {
      MoveBack();
      delay(100); resetFunc();
    }
      break;
    case 2: Serial.println("BLACK");
     while(1)
    {
      MoveBack();
      delay(100); resetFunc();
    }
      break;
    case 6:
      Serial.println("rute RED");//RUTE MERAH
      jalan_merah();
      Stop();
      Serial.println("FINISH");
      delay(100);
      break;/////////////////AKHIR DARI RUTE MERAH
    case 8:
      Serial.println("rute hijau");//RUTE HIJAU
      jalan_ijo();
      Stop();
      Serial.println("FINISH");
      delay(100);
      exit(0);
      break;///////////////////////AKHIR DARI RUTE HIJAU
    case 7:
      Serial.println("rute biru");//RUTE BIRU
      jalan_biru();
      delay(200);
      break;////////////////////////////////AKHIR DARI RUTE BIRU
      exit(0);
    default: Serial.println("unknown");
     while(1)
    {
      MoveBack();
      delay(100); resetFunc();
    }
      break;
      //readColor();//read sensor
      //decideColor();//format color values
      //printColor();//print values
  }
}

void decideColor() {//format color values
  //Limit possible values:
  redColor = constrain(redColor, 0, 255);
  greenColor = constrain(greenColor, 0, 255);
  blueColor = constrain(blueColor, 0, 255);

  //find brightest color:
  int maxVal = max(redColor, blueColor);
  maxVal = max(maxVal, greenColor);
  //map new values
  redColor = map(redColor, 0, maxVal, 0, 255);
  greenColor = map(greenColor, 0, maxVal, 0, 255);
  blueColor = map(blueColor, 0, maxVal, 0, 255);
  redColor = constrain(redColor, 0, 255);
  greenColor = constrain(greenColor, 0, 255);
  blueColor = constrain(blueColor, 0, 255);

  //light led
  //decide which color is present (you may need to change some values here):
  if (redColor > 250 && greenColor > 250 && blueColor > 250) {
    color = 1;//white
  }
  else if (redColor < 25 && greenColor < 25 && blueColor < 25) {
    color = 2;//black
  }
  else if (redColor > 250 && greenColor < 200 && blueColor < 200) {
    color = 6;//red
    warna = 6;
    iro = 6;
    firstLoop_B = false;//iki nggarakno mlaku pisan tok
    secondLoop_B = false;
    thirdLoop_B = false;
    fourthLoop_B = false;

    firstLoop_G = false;//iki nggarakno mlaku pisan tok
    secondLoop_G = false;
    thirdLoop_G = false;
    fourthLoop_G = false;

  }
  else if (redColor < 240 && greenColor < 240 && blueColor > 250) {
    color = 7;//blue
    warna = 7;
    iro = 7;
    firstLoop_R = false;//iki nggarakno mlaku pisan tok
    secondLoop_R = false;
    thirdLoop_R = false;
    fourthLoop_R = false;

    firstLoop_G = false;//iki nggarakno mlaku pisan tok
    secondLoop_G = false;
    thirdLoop_G = false;
    fourthLoop_G = false;
  }
  else if (redColor < 230 && greenColor > 250 && blueColor < 230) {
    color = 8;//green
    warna = 8;
    iro = 8;

    firstLoop_R = false;//iki nggarakno mlaku pisan tok
    secondLoop_R = false;
    thirdLoop_R = false;
    fourthLoop_R = false;

    firstLoop_B = false;//iki nggarakno mlaku pisan tok
    secondLoop_B = false;
    thirdLoop_B = false;
    fourthLoop_B = false;
  }
  else {
    color = 0;//unknown
  }
}


void calibrate() {
  Serial.println("Calibrating...");
  Serial.println("White");//aim sensor at something white
  //set calibration vaues:
  delay(1000);
  digitalWrite(S2, LOW);
  digitalWrite(S3, LOW);
  redMin = pulseIn(sensorOut, LOW);
  delay(100);
  digitalWrite(S2, HIGH);
  digitalWrite(S3, HIGH);
  greenMin = pulseIn(sensorOut, LOW);
  delay(100);
  digitalWrite(S2, LOW);
  digitalWrite(S3, HIGH);
  blueMin = pulseIn(sensorOut, LOW);
  delay(100);
  MoveForward();
  delay(250);
  Stop();
  delay(500);
  Serial.println("next...");//aim sensor at something black
  delay(1000);
  Serial.println("Black");
  //set calibration values:
  digitalWrite(S2, LOW);
  digitalWrite(S3, LOW);
  redMax = pulseIn(sensorOut, LOW);
  delay(100);
  digitalWrite(S2, HIGH);
  digitalWrite(S3, HIGH);
  greenMax = pulseIn(sensorOut, LOW);
  delay(100);
  digitalWrite(S2, LOW);
  digitalWrite(S3, HIGH);
  blueMax = pulseIn(sensorOut, LOW);
  delay(100);
  Serial.println("Done calibrating.");
  delay(1000);
  MoveForward();
  delay(150);
  Stop();
  delay(50);
}

void printColor() {//print data
  Serial.print("R = ");
  Serial.print(redColor);
  Serial.print(",");
  Serial.print(" G = ");
  Serial.print(greenColor);
  Serial.print(",");
  Serial.print(" B = ");
  Serial.print(blueColor);
  Serial.print(",");
  Serial.print(" Color: ");

  switch (color) {
    case 1: Serial.println("WHITE");
      break;
    case 2: Serial.println("BLACK");
      break;
    case 6: Serial.println("RED");
      break;
    case 7: Serial.println("BLUE");
      break;
    case 8: Serial.println("GREEN");
      break;
    default: Serial.println("unknown");
      break;
  }

}

void readColor() {//get data from sensor
  //red:
  digitalWrite(S2, LOW);
  digitalWrite(S3, LOW);
  redFrequency = pulseIn(sensorOut, LOW);
  redColor = map(redFrequency, redMin, redMax, 255, 0);
  delay(100);

  //green:
  digitalWrite(S2, HIGH);
  digitalWrite(S3, HIGH);
  greenFrequency = pulseIn(sensorOut, LOW);
  greenColor = map(greenFrequency, greenMin, greenMax, 255, 0);
  delay(100);

  //blue:
  digitalWrite(S2, LOW);
  digitalWrite(S3, HIGH);
  blueFrequency = pulseIn(sensorOut, LOW);
  blueColor = map(blueFrequency, blueMin, blueMax, 255, 0);
  delay(100);
}

void MoveForward(void)
{


  digitalWrite(LM1, LOW);
  digitalWrite(LM2, HIGH);
  digitalWrite(RM1, LOW);
  digitalWrite(RM2, HIGH);
}

void MoveBack(void)
{


  digitalWrite(LM1, HIGH);
  digitalWrite(LM2, LOW);
  digitalWrite(RM1, HIGH);
  digitalWrite(RM2, LOW);
}

void MoveSRight(void)
{
  digitalWrite(LM1, HIGH);
  digitalWrite(LM2, LOW);
  digitalWrite(RM1, LOW);
  digitalWrite(RM2, HIGH);
}

void MoveSLeft(void)
{

  digitalWrite(LM1, LOW);
  digitalWrite(LM2, HIGH);
  digitalWrite(RM1, HIGH);
  digitalWrite(RM2, LOW);
}

void MoveRight(void)
{


  digitalWrite(LM1, LOW);
  digitalWrite(LM2, LOW);
  digitalWrite(RM1, LOW);
  digitalWrite(RM2, HIGH);

}

void MoveLeft(void)
{


  digitalWrite(LM1, LOW);
  digitalWrite(LM2, HIGH);
  digitalWrite(RM1, LOW);
  digitalWrite(RM2, LOW);
}

void Stop(void)
{
  digitalWrite(LM1, LOW);
  digitalWrite(LM2, LOW);
  digitalWrite(RM1, LOW);
  digitalWrite(RM2, LOW);
}

void jalan_biru(void)
{
  MoveForward();
  delay(300);
  MoveSRight();
  delay(190);
  MoveForward();
  delay(580);
  MoveSLeft();
  delay(250);
  MoveForward();
  delay(150);
  while(1)
  {
    mlaku();  
  }
  
}
void jalan_merah(void)
{
  MoveForward();
  delay(300);
  MoveSLeft();
  delay(250);
  MoveForward();
  delay(700);
  MoveSRight();
  delay(250);
  MoveForward();
  delay(150);
  while(1){
    mlaku();  
  }
}
void jalan_ijo()
{
  MoveForward();
  delay(550);
  Stop();
  delay(5);
  while(1)
  {
    mlaku();
  }
    
}

void mlaku(void)
{
  Sensor1 = analogRead(Out1);
  Sensor2 = analogRead(Out2);
  Sensor3 = analogRead(Out3);
  Sensor4 = analogRead(Out4);
  Sensor5 = analogRead(Out5);
  Sensor6 = analogRead(Out6);


  // White = 0
  // Black = 1

  Sensor1 = Sensor1 < THRESHOLD ? 0 : 1;
  Sensor2 = Sensor2 < THRESHOLD ? 0 : 1;
  Sensor3 = Sensor3 < THRESHOLD ? 0 : 1;
  Sensor4 = Sensor4 < THRESHOLD ? 0 : 1;
  Sensor5 = Sensor5 < THRESHOLD ? 0 : 1;
  Sensor6 = Sensor6 < THRESHOLD ? 0 : 1;

  if (!Sensor1 && !Sensor6) //  2 sensor work
  {
    if (!Sensor2 && !Sensor3 && !Sensor4 && !Sensor5)
      MoveBack();
    else {
      if (Sensor3 || Sensor4)
        MoveForward();
      else if (Sensor5 && !Sensor2)
        MoveRight();
      else if (!Sensor5 && Sensor2 )
        MoveLeft();
      else
        MoveBack();
    }
  }

  else {
    if ((Sensor2 && Sensor1))
      MoveSLeft();  //for checkpoints
    else if ((Sensor4 && Sensor5 && Sensor6))
      MoveSRight();
    else if ((Sensor1 && Sensor2 && Sensor3))
      MoveSLeft();
    else if ((!Sensor4 && !Sensor5 && !Sensor6))
      MoveSLeft();
    else if ((!Sensor1 && !Sensor2 && !Sensor3))
      MoveSRight();
    else if ((Sensor3 || Sensor4))
      MoveForward();
    else if ((Sensor6 && Sensor5))
      MoveSRight();
    else
      MoveBack();
  }
  delay(5);

  if (Sensor2 && Sensor3 && Sensor4 && Sensor5 && Sensor1 && Sensor6)
  {
    
    if (firstLoop_R) {
      merah_awal();
      firstLoop_R = false;
    }

    else if (secondLoop_R) {
      pilihan_mbalik_R();
      secondLoop_R = false;
    }

    else if (thirdLoop_R) {
      mbalik_pertigaan_R();
      thirdLoop_R = false;
    }

    else if (fourthLoop_R) {
      mbalik_start_R();
      fourthLoop_R = false;
    }

    else if (firstLoop_B) {
      biru_awal();
      firstLoop_B = false;
    }

    else if (secondLoop_B) {
      pilihan_mbalik_B();
      secondLoop_B = false;
    }

    else if (thirdLoop_B) {
      mbalik_pertigaan_B();
      thirdLoop_B = false;
    }

    else if (fourthLoop_B) {
      mbalik_start_B();
      fourthLoop_B = false;
    }

    else if (firstLoop_G) {
      ijo_awal();
      firstLoop_G = false;
    }

    else if (secondLoop_G) {
      pilihan_mbalik_G();
      secondLoop_G = false;
    }

     else if (thirdLoop_G) {
      mbalik_pertigaan_G();
      thirdLoop_G = false;
    }


    else if (fourthLoop_G) {
      mbalik_start_G();
      fourthLoop_G = false;
    }
    Stop();

  }

  delay(5);
}

void milih(void)
{
  Serial.println("sek urung dadi");
}

void merah_awal(void) {
  Stop();
  delay(1000);
  MoveForward();//jalan Merah
  delay(300);
  MoveSLeft();
  delay(260);
  MoveForward();
  delay(450);
  mlaku();
}

void biru_awal(void) {
  Stop();
  delay(1000);
  MoveForward();//jalan biru
  delay(300);
  MoveSRight();
  delay(260);
  MoveForward();
  delay(450);
  mlaku();
}

void ijo_awal(void) {
  Stop();
  delay(1000);
  MoveForward();//jalan Merah
  delay(500);
  MoveSRight();
  delay(25);
  MoveForward();//jalan Merah
  delay(100);
  mlaku();
}

void pilihan_mbalik_R(void)
{
  MoveForward();
  delay(300);
  Stop();
  delay(5000);//putar balik
  MoveSLeft();
  delay(530);
  MoveForward();
  delay(500);
  mlaku();
}

void pilihan_mbalik_B(void)
{
  MoveForward();
  delay(300);
  Stop();
  delay(5000);//putar balik
  MoveSLeft();
  delay(530);
  MoveForward();
  delay(500);
  mlaku();
}

void pilihan_mbalik_G(void)
{
  MoveForward();
  delay(300);
  Stop();
  delay(5000);//putar balik
  MoveSLeft();
  delay(530);
  MoveForward();
  delay(400);
  MoveSRight();
  delay(25);
  MoveForward();
  delay(100);
  mlaku();
}

void mbalik_pertigaan_B(void)
{
  Stop();
  delay(500);
  MoveForward();
  delay(250);
  MoveSLeft();
  delay(250);
  MoveForward();
  delay(400);
  mlaku();
}

void mbalik_pertigaan_R(void)
{
  Stop();
  delay(500);
  MoveForward();
  delay(250);
  MoveSRight();
  delay(250);
  MoveForward();
  delay(400);
  mlaku();
}


void mbalik_pertigaan_G(void)
{
  MoveForward();
  delay(500);
  MoveSLeft();
  delay(25);
  mlaku();
}

void mbalik_start_B(void)
{
  Stop();
  delay(500);
  MoveForward();
  delay(150);
  MoveSRight();
  delay(250);
  MoveForward();
  delay(150);
  mlaku();
}

void mbalik_start_R(void)
{
  Stop();
  delay(500);
  MoveForward();
  delay(150);
  MoveSLeft();
  delay(250);
  MoveForward();
  delay(150);
  mlaku();
}

void mbalik_start_G(void)
{
  Stop();
  delay(500);
  MoveForward();
  delay(150);
  mlaku();
}
