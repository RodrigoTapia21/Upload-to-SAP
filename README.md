REPORT Z_PRUEBA_TP16.

DATA: lt_socios TYPE TABLE OF ZSOCIOS,
      ls_socios TYPE ZSOCIOS,
      lv_filename TYPE string.

lv_filename = 'C:\Documents and Settings\Administrator\Desktop\EXCEL DE PRUEBA.CSV'.

CALL FUNCTION 'GUI_UPLOAD'
  EXPORTING
    filename                      = lv_filename
    filetype                      = 'ASC'
  TABLES
    data_tab                      = lt_socios
  EXCEPTIONS
    file_open_error               = 1
    file_read_error               = 2
    no_batch                      = 3
    gui_refuse_filetransfer       = 4
    invalid_type                  = 5
    no_authority                  = 6
    unknown_error                 = 7
    bad_data_format               = 8
    header_not_allowed            = 9
    separator_not_allowed         = 10
    header_too_long               = 11
    unknown_dp_error              = 12
    access_denied                 = 13
    dp_out_of_memory              = 14
    disk_full                     = 15
    dp_timeout                    = 16
    OTHERS                        = 17.

IF sy-subrc <> 0.
  MESSAGE ID sy-msgid TYPE sy-msgty NUMBER sy-msgno
          WITH sy-msgv1 sy-msgv2 sy-msgv3 sy-msgv4.
ENDIF.

LOOP AT lt_socios INTO ls_socios.
  INSERT INTO ZSOCIOS VALUES ls_socios.
ENDLOOP.
