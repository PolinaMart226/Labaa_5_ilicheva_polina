# Лабораторная работа №5. Хранение данных. Настройки и внешние файлы.
**Язык программирования**: Java  
**Выполнила**: Ильичева П.Е.

**Цель работы**
Изучить инструменты хранения данных, а также работу с внешними 
файлами. 

## Задания лабораторной работы 
**Задание 1.**  
Изучите пример подключения к сети. 

`public void myClickHandler(View view) {` 

`...` 

`ConnectivityManager connMgr = (ConnectivityManager)` 

`getSystemService(Context.CONNECTIVITY_SERVICE);` 

`NetworkInfo networkInfo = connMgr.getActiveNetworkInfo();`

`if (networkInfo != null && networkInfo.isConnected()) {`

`// fetch data` 

`} else {`

`// display error` 

`}`

`...` 

`}`

**Задание 2.**
Изучите код приложений 

**HttpURLConnection**

`private String downloadUrl(String myurl) throws IOException {`

`InputStream is = null;`

`// Only display the first 500 characters of the retrieved` 

`// web page content.` 

`int len = 500;` 

`try {`

`URL url = new URL(myurl);` 

`HttpURLConnection conn = (HttpURLConnection) url.openConnection();`

`conn.setReadTimeout(10000 /* milliseconds */);` 

`conn.setConnectTimeout(15000 /* milliseconds */);` 

`conn.setRequestMethod("GET"); conn.setDoInput(true);`

`// Starts the query conn.connect();` 

`int response = conn.getResponseCode();` 

`Log.d(DEBUG_TAG, "The response is: " + response); is = conn.getInputStream();` 

`// Convert the InputStream into a string` 

`String contentAsString = readIt(is, len);` 

`return contentAsString;` 

`// Makes sure that the InputStream is closed after the app is` 

`// finished using it.` 

`} finally {`

`if (is != null) {` 

`is.close();` 

`}` 

`}` 

`}`

**Преобразование полученной информации к типу Srting**

`public String readIt (InputStream stream, int len) throws IOException,` 

`UnsupportedEncodingException {` 

`Reader reader = null; `

`reader = new InputStreamReader(stream, "UTF-8");` 

`char[] buffer = new char[len];`

`reader.read(buffer);`

`return new String(buffer);` 

`}`

**Http GET запрос**

- Создаем HttpClient 

`HttpClient client = new DefaultHttpClient();` 

- Создаем объект HttpGet 

`HttpGet request = new HttpGet("http://www.example.com");` 

- Выполняем HTTP запрос 
`HttpResponse response;`

`try {` 

`response = client.execute(request);` 

`Log.d("Response of GET request", response.toString());` 

`} catch (ClientProtocolException e) {` 

`// TODO Auto-generated catch block` 

`e.printStackTrace();` 

`} catch (IOException e) {`

`// TODO Auto-generated catch block` 

`e.printStackTrace();` 

`}` 

**Взаимодействие с сервером через сокеты**

`public class Requester extends Thread {` 

`Socket requestSocket;` 

`String message;` 

`StringBuilder returnStringBuffer = new StringBuilder();` 

`Message lmsg;` 

`int ch;` 

`@Override public void run() {` 

`try {` 

`this.requestSocket = new Socket("remote.servername.com",13);` 

`InputStreamReader isr = new` 

`InputStreamReader(this.requestSocket. getInputStream(), "ISO-8859-1");` 

`while ((this.ch = isr.read()) != -1) {` 

`this.returnStringBuffer.append((char) this.ch);` 

`}` 

`this.message = this.returnStringBuffer.toString();` 

`this.lmsg = new Message();` 

`this.lmsg.obj = this.message;` 

`this.lmsg.what = 0;` 

`h.sendMessage(this.lmsg);` 

`this.requestSocket.close();` 

`}` 

`catch (Exception ee) {` 

`Log.d("sample application", "failed to read data" + ee.getMessage());` 

`}` 

`}` 

`}`

**Задание 3.** Работа с внешними файлами.

Разработать мобильное приложение, позволяющее пользователю асинхронно скачивать файлы журнала Научно-технический вестник. 
Файлы хранятся на сервере в формате PDF и расположены по адресу: http://ntv.ifmo.ru/file/journal/идентификатор_журнала.pdf 
Не для всех ID имеются журналы, поэтому необходимо предусмотреть сообщение об отсутствии файла. В случае если файл не найден, 
ответ от сервера будет содержать главную страницу сайта. 
Определить существует ли файл можно по возвращаемому сервером заголовку (параметр content-type). 
Примеры ссылок: 
http://ntv.ifmo.ru/file/journal/1.pdf – возвращен PDF файл 
http://ntv.ifmo.ru/file/journal/2.pdf – файл не найден, возвращена главная страница сайта 
Файлы должны храниться на устройстве в папке, создаваемой при первом запуске приложения (путь до папки и ее название определите самостоятельно). 
После окончания загрузки файла должна становиться доступной кнопка «Смотреть» и кнопка «Удалить». 
При нажатии на кнопку «Смотреть» должно происходить открытие сохраненного на устройстве файла.
Предусмотреть ошибку, если на устройстве не установлено приложение, открывающее PDF файлы. 
При нажатии на кнопку «Удалить» загруженный файл должен удаляться с устройства.
**Выполненное задние:**


https://github.com/user-attachments/assets/48fa7281-40ca-4380-a946-d696010509b9


**Задание 4.** Хранение и чтение настроек.

При запуске приложения пользователю должно выводиться всплывающее полупрозрачное уведомление (popupWindow),
с краткой инструкцией по использованию приложения (можете написать случайный текст),
чекбоксом «Больше не показывать» и кнопкой «ОК».
Если чекбокс был отмечен и нажата кнопка ОК, необходимо произвести сохранение данного параметра используя SharedPreferences.
При следующем запуске приложения производить проверку параметра, и не выводить всплывающее сообщение, если чекбокс был отмечен.
**Выполненное задние:**

https://github.com/user-attachments/assets/6604b215-c1c0-4ce0-8ede-c73161ec3d5f



