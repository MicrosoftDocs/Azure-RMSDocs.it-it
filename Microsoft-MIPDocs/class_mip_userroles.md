# <a name="class-mipuserroles"></a>Classe mip::UserRoles 
Rappresenta un gruppo di utenti e i ruoli ad essi associati.
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public MIP_EXPORT UserRolesUserList & users,const RoleList & roles) public inline const UserList & Users | Ottiene gli utenti associati a un set di ruoli.
public inline const RoleList & Roles | Ottiene i ruoli associati a un gruppo di utenti.
## <a name="members"></a>Membri
### <a name="userroles"></a>UserRoles
Costruttore [UserRoles](#classmip_1_1_user_roles).
#### <a name="parameters"></a>Parametri
* users Gruppo di utenti che condividono gli stessi ruoli 
* roles [Ruoli](#classmip_1_1_roles) condivisi dal gruppo di utenti
### <a name="userlist"></a>UserList
Ottiene gli utenti associati a un set di ruoli.
#### <a name="returns"></a>Returns
Utenti associati a un set di ruoli
### <a name="rolelist"></a>RoleList
Ottiene i ruoli associati a un gruppo di utenti.
#### <a name="returns"></a>Returns
[Ruoli](#classmip_1_1_roles) associati a un gruppo di utenti