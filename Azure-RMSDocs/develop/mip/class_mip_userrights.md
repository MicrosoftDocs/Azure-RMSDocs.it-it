# <a name="class-mipuserrights"></a>Classe mip::UserRights 
Rappresenta un gruppo di utenti e i diritti ad essi associati.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public inline  UserRightsUserList & users,const RightList & rights) public inline const UserList & Users | Ottiene gli utenti associati a un set di diritti.
public inline const RightList & Rights | Ottiene i diritti associati a un gruppo di utenti.
## <a name="members"></a>Membri
### <a name="userrights"></a>UserRights
Costruttore [UserRights](#classmip_1_1_user_rights).
#### <a name="parameters"></a>Parametri
* users Gruppo di utenti che condividono gli stessi diritti 
* rights Diritti condivisi dal gruppo di utenti
### <a name="userlist"></a>UserList
Ottiene gli utenti associati a un set di diritti.
#### <a name="returns"></a>Returns
Utenti associati a un set di diritti
### <a name="rightlist"></a>RightList
Ottiene i diritti associati a un gruppo di utenti.
#### <a name="returns"></a>Returns
Diritti associati a un gruppo di utenti