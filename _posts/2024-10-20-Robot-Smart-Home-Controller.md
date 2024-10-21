## Robot Smart Home Controller
### Code reorganization and breakages

I am in the midst of a complete reorganiation of the code base. There is a breakage in new code. I am trying to
initializ an array of structs, which is not working right now. I do not yet understand what I am doing wrong,
but the Arduino IDE is not happy with me.

The following are code exerpts I am working with. I am pretty sure I am not supposed to be initializing the
array if Web_Page_Infor structs this way. I might have to define the array and initialize it in setup().

```
struct Web_Page_Info {
  uint8_t id;
  String html;
  String name;
  String title;
};

Web_Page_Info Web_Pages[MAX_NUM_INFO_PAGES] = 
{
  { PAGE_HOME_ID, String(HTML_CONTENT_HOME), PAGE_HOME_NAME, PAGE_HOME_TITLE },
  { PAGE_ENVIRONMENT_ID, String(HTML_CONTENT_ENVIRONMENT), PAGE_ENVIRONMENT_NAME, PAGE_ENVIRONMENT_TITLE },
  { PAGE_SWITCHES_ID, String(HTML_CONTENT_SWITCHES), PAGE_SWITCHES_NAME, PAGE_SWITCHES_TITLE },
  { PAGE_POTENTIOMETER_ID, String(HTML_CONTENT_POTENTIOMETER), PAGE_POTENTIOMETER_NAME, PAGE_POTENTIOMETER_TITLE },
  { PAGE_LIGHT_ID, String(HTML_CONTENT_LIGHT), PAGE_LIGHT_NAME, PAGE_LIGHT_TITLE },
  { PAGE_IMU_BNO055_ID, String(HTML_CONTENT_IMU_BNO055), PAGE_IMU_BNO055_NAME, PAGE_IMU_BNO055_TITLE },
  { PAGE_IMU_LSM6DSOX_ID, String(HTML_CONTENT_IMU_LSM6DSOX), PAGE_IMU_LSM6DSOX_NAME, PAGE_IMU_LSM6DSOX_TITLE },
  { PAGE_NO_DATA_ID, String(HTML_CONTENT_NO_DATA), PAGE_NO_DATA_NAME, PAGE_NO_DATA_TITLE },
  { PAGE_ERROR_404_ID, String(HTML_CONTENT_404), PAGE_ERROR_404_NAME, PAGE_ERROR_404_TITLE },
  { PAGE_ERROR_405_ID, String(HTML_CONTENT_405), PAGE_ERROR_405_NAME, PAGE_ERROR_405_TITLE }
};
