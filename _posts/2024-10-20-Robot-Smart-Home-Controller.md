## Robot Smart Home Controller
### Code Reorganization and Breakages

I am in the midst of a complete reorganiation of the code base. There is a breakage in new code. I am trying to
initializ an array of structs, which is not working right now. I do not yet understand what I am doing wrong,
but the Arduino IDE is not happy with me.

The following are code exerpts I am working with. I am pretty sure I am not supposed to be initializing the
array if Web_Page_Infor structs this way. I might have to define the array and initialize it in setup().

{% highlight arduino %}```
#define INFO_PAGE_BASE                0

#define PAGE_HOME_ID                  INFO_PAGE_BASE
#define PAGE_HOME_NAME                "Robot Smart Home Controller"
#define PAGE_HOME_TITLE               PAGE_HOME_NAME

#define PAGE_ENVIRONMENT_ID           INFO_PAGE_BASE + 1
#define PAGE_ENVIRONMENT_NAME         "Robot Smart Home Controller: Environment"
#define PAGE_ENVIRONMENT_TITLE        PAGE_ENVIRONMENT_NAME

#define PAGE_SWITCHES_ID              INFO_PAGE_BASE + 2
#define PAGE_SWITCHES_NAME            "Robot Smart Home Controller: Switches"
#define PAGE_SWITCHES_TITLE           PAGE_SWITCHES_NAME

#define PAGE_POTENTIOMETER_ID         INFO_PAGE_BASE + 3
#define PAGE_POTENTIOMETER_NAME       "Robot Smart Home Controller: Potentiometer"
#define PAGE_POTENTIOMETER_TITLE      PAGE_POTENTIOMETER_NAME

#define PAGE_LIGHT_ID                 INFO_PAGE_BASE + 4
#define PAGE_LIGHT_NAME               "Robot Smart Home Controller: Light/Lux"
#define PAGE_LIGHT_TITLE              PAGE_LIGHT_NAME

#define PAGE_IMU_BNO055_ID            INFO_PAGE_BASE + 5
#define PAGE_IMU_BNO055_NAME          "Robot Smart Home Controller: BNO055 IMU"
#define PAGE_IMU_BNO055_TITLE         PAGE_IMU_BNO055_NAME

#define PAGE_IMU_LSM6DSOX_ID          INFO_PAGE_BASE + 6
#define PAGE_IMU_LSM6DSOX_NAME        "Robot Smart Home Controller: LSM6DSOX IMU"
#define PAGE_IMU_LSM6DSOX_TITLE       PAGE_IMU_LSM6DSOX_NAME

#define PAGE_NO_DATA_ID               INFO_PAGE_BASE + 7
#define PAGE_NO_DATA_NAME             "Robot Smart Home Controller: NO DATA AVAILABLE"
#define PAGE_NO_DATA_TITLE            PAGE_NO_DATA_NAME

#define PAGE_ERROR_404_ID             INFO_PAGE_BASE + 8
#define PAGE_ERROR_404_NAME           "Page Not Found"
#define PAGE_ERROR_404_TITLE          PAGE_ERROR_404_NAME

#define PAGE_ERROR_405_ID             INFO_PAGE_BASE + 9
#define PAGE_ERROR_405_NAME           "Unknown"
#define PAGE_ERROR_405_TITLE          PAGE_ERROR_405_NAME

#define LAST_INFO_PAGE_ID             PAGE_ERROR_405_ID

#define MAX_NUM_INFO_PAGES            LAST_INFO_PAGE_ID + 1

struct Web_Page_Info {
  uint8_t id;
  String html;
  String name;
  String title;
};

Web_Page_Info Web_Pages[MAX_NUM_INFO_PAGES] = 
{
  { PAGE_HOME_ID, "", PAGE_HOME_NAME, PAGE_HOME_TITLE },
  { PAGE_ENVIRONMENT_ID, "", PAGE_ENVIRONMENT_NAME, PAGE_ENVIRONMENT_TITLE },
  { PAGE_SWITCHES_ID, "", PAGE_SWITCHES_NAME, PAGE_SWITCHES_TITLE },
  { PAGE_POTENTIOMETER_ID, "", PAGE_POTENTIOMETER_NAME, PAGE_POTENTIOMETER_TITLE },
  { PAGE_LIGHT_ID, "", PAGE_LIGHT_NAME, PAGE_LIGHT_TITLE },
  { PAGE_IMU_BNO055_ID, "", PAGE_IMU_BNO055_NAME, PAGE_IMU_BNO055_TITLE },
  { PAGE_IMU_LSM6DSOX_ID, "", PAGE_IMU_LSM6DSOX_NAME, PAGE_IMU_LSM6DSOX_TITLE },
  { PAGE_NO_DATA_ID, "", PAGE_NO_DATA_NAME, PAGE_NO_DATA_TITLE },
  { PAGE_ERROR_404_ID, "", PAGE_ERROR_404_NAME, PAGE_ERROR_404_TITLE },
  { PAGE_ERROR_405_ID, "", PAGE_ERROR_405_NAME, PAGE_ERROR_405_TITLE }
};

/*
  Set up the empty page for when there is no data - sensor is not
    available.
*/
String set_empty_page (QWIICMUX mx, Web_Page_Info page_info, uint16_t sequence_nr) {
  String date_time, html;

  html =  page_info[PAGE_NO_DATA_ID].html;    // Line 523
  date_time = timestamp(mx, page_info[PAGE_NO_DATA_ID].name, SHOW_FULL_DATE, SHOW_12_HOURS, SHOW_LONG_DATE, SHOW_SECONDS);
  Serial.println(page_info[PAGE_NO_DATA_ID].name);
  html.replace("PAGE_NAME_MARKER", page_info[PAGE_NO_DATA_ID].name);
  html.replace("DATESTAMP_MARKER", date_time);
  html.replace("SEQUENCE_COUNT_MARKER", String(sequence_nr));

  return html;
}
(% endhighlight %}

