# configura
     /*******************************************************************/
     /*Author      : Wan Chun Man                                        */
     /*Program Name: KCFBACKUP                                           */
     /*Description : Configura Programming Challenge(File Backup Utility)*/
     /*Date        : 15.12.2017                                          */
     /********************************************************************/
             PGM        PARM(&CMDPRM)
    /*VARIABLE SECTION?/
             DCL        VAR(&CMDPRM) TYPE(*CHAR) LEN(20)
             DCL        VAR(&FILENM) TYPE(*CHAR) LEN(10)
             DCL        VAR(&MBRNAM) TYPE(*CHAR) LEN(10)
             DCL        VAR(&DATE)   TYPE(*CHAR) LEN(8)
             DCL        VAR(&DATE1)  TYPE(*CHAR) LEN(8)

    /*FILE DECLARATION */
             DCLF       FILE(BACKUP) OPNID(BACKUP)

    /*RETRIEVE DATE      */
             CHGVAR     VAR(&DATE)   VALUE(%SST(&CMDPRM 11 8))

    /*VALIDATE DATE      */
             CVTDAT     DATE(&DATE) TOVAR(&DATE1) TOFMT(*DMY)
             MONMSG     MSGID(CPF0555 CPF0552) EXEC(DO)
             SNDUSRMSG  MSG('The Date Is Invalid. Please key in a +
                          valid date. Thanks.')
             GOTO       CMDLBL(ENDPGM)
             ENDDO

    /*RETRIEVE FILE NAME */
             CHGVAR     VAR(&FILENM) VALUE(%SST(&CMDPRM 1 10))

    /*RETRIEVE MEMBER NAME */
             CHGVAR     VAR(&MBRNAM) VALUE('BKUP' *TCAT &DATE)

    /*COPY TO BACKUP FILE */
             CPYF       FROMFILE(&FILENM) TOFILE(BACKUP) +
                        TOMBR(&MBRNAM) +
                        MBROPT(*REPLACE) FMTOPT(*NOCHK)
             MONMSG     MSGID(CPF2817) EXEC(DO)
             CPYF       FROMFILE(&FILENM) TOFILE(BACKUP) +
                        TOMBR(&MBRNAM) +
                        MBROPT(*ADD) FMTOPT(*NOCHK)
             GOTO       ENDPGM
             ENDDO
 ENDPGM:     ENDPGM
