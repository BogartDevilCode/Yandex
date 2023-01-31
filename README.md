# для Yandex
Этот модуль( в котором описывается класс )  был написан в IDE DevelNext. Часть моего кода по проекту, здесь описываются функции, которые в дальнейшем используется по назначению. Присутствуют циклы и логические операторы, SQL - запросы. 
MainModule

`<?php
namespace app\modules;

use Exception;
use std, gui, framework, app;


class MainModule extends AbstractModule
{

    /**
     * @event database.error 
     */
    function doDatabaseError(ScriptEvent $e = null)
    {    
       UXDialog::show("Подсоединение по адресу: ". $this->database->host . ":" . $this->database->port . " отклонено. Проверьте что хост и порт указаны правильно и что postmaster принимает TCP/IP-подсоединения.", 'ERROR');
    }

    /**
     * @event database.open 
     */
    function doDatabaseOpen(ScriptEvent $e = null)
    {
      $this->labelinfo->text = $this->database->host;    
    }

    /**
     * @event mail.send 
     */
    function doMailSend(ScriptEvent $e = null)
    {    
        pre("ок");
    }

    /**
     * @event mail.error 
     */
    function doMailError(ScriptEvent $e = null)
    {    
        pre("Ошибка");
    }

    /**
     * @event mailAlt.send 
     */
    function doMailAltSend(ScriptEvent $e = null)
    {    
        pre("Активировано");
        $this->buttonAlt->enabled = true;
        $this->button->enabled = false;
    }

    /**
     * @event mailAlt.error 
     */
    function doMailAltError(ScriptEvent $e = null)
    {    
        pre("Ошибка доступа".$e);
    }

    /**
     * @event timer.action 
     */
    function doTimerAction(ScriptEvent $e = null)
    {    
           $ii = -1;
           foreach ($this->table->items as $item){
                   $ii += 1;
                   if (str::contains($item[""."rpo".""], "3") == true){
                      $i = $i . "1";
                      $this->table->selectedIndex = $ii;
                      
                   }
           }
           $length = str::length($i);
           if ($length > 0){
               $email = $this->ini3->get('email');
               $this->mailAlt->send(['to' => $email,
                          'message' => "[MODULE] - Внимание! Обнаружен класс пожарной пасности 3",
                          'subject' => "3 КПО"
               ]);
               
           }
           $ii = -1;
           foreach ($this->table->items as $item){
                   $ii += 1;
                   if (str::contains($item[""."rpo".""], "4") == true){
                      $i = $i . "1";
                      $this->table->selectedIndex = $ii;
                      
                   }
           }
           $length = str::length($i);
           if ($length > 0){
               $email = $this->ini3->get('email');
               $this->mailAlt->send(['to' => $email,
                          'message' => "[MODULE] - Внимание! Обнаружен класс пожарной пасности 4",
                          'subject' => "4 КПО"
               ]);
               
           }
           $ii = -1;
           foreach ($this->table->items as $item){
                   $ii += 1;
                   if (str::contains($item[""."rpo".""], "5") == true){
                      $i = $i . "1";
                      $this->table->selectedIndex = $ii;
                      
                   }
           }
           $length = str::length($i);
           if ($length > 0){
               $email = $this->ini3->get('email');
               $this->mailAlt->send(['to' => $email,
                          'message' => "[MODULE] - Внимание! Обнаружен класс пожарной пасности 5",
                          'subject' => "5 КПО"
               ]);
               
           }
           $ii = -1;
           $scan = $this->tempmm->text;
           foreach (app()->form('meteomon')->table->items as $item){
                   $ii += 1;
                   if (str::contains($item[""."temp_b".""], $scan) == true){
                      $i = $i . "1";
                      app()->form('meteomon')->table->selectedIndex = $ii;                   
                   }
           }
           $length = str::length($i);
           if ($length > 0){
               $email = $this->ini3->get('email');
               $this->mailAlt->send(['to' => $email,
                          'message' => "[MODULE] - Внимание! Сработало ограничение! Проверьте метео-модуль",
                          'subject' => "Температура достигла предела по ограничению"
               ]);
               
           }
    }

    /**
     * @event timerAlt.action 
     */
    function doTimerAltAction(ScriptEvent $e = null)
    {    
        $this->reloadUsersStart();
    }

    
    function getUsers()
    {
        return $this->database->query('select * from meteo_data order by id desc');
    }
    
    function getData()
    {
        return $this->database->query('select * from tableforest order by id desc');
    }
    
    function getDataS()
    {
        return $this->database->query('select * from radiation order by id desc');
    }
    
    function deleteUser($id)
    {
        return $this->database->query('delete from tableforest where id = ?', [$id])->update();
    }
    
    function getUsersTable()
    {
        return $this->database->query('select * from firehazard order by id desc');
    }
    
    function getUsersTable_Coeff()
    {
        return $this->database->query('select * from coefficient_nestorov order by id desc');
    }
    
    function Autorization($login, $password){
        return $this->database->query('SELECT login,password FROM account WHERE login=? and password=?', [$login, $password]);
    }
    

}`
