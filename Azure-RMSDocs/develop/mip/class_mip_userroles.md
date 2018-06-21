# <a name="class-mipuserroles"></a>Classe mip::UserRoles 
Rappresenta un gruppo di utenti e i ruoli ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
 public MIP_EXPORT UserRoles(const UserList& users, const RoleList& roles)  |  Costruttore [UserRoles](class_mip_userroles.md).
 public const UserList& Users() const  |  Ottiene gli utenti associati a un set di ruoli.
 public const RoleList& Roles() const  |  Ottiene i ruoli associati a un gruppo di utenti.
  
## <a name="members"></a>Membri
  
### <a name="userroles"></a>UserRoles
Costruttore [UserRoles](class_mip_userroles.md).

Parametri:  
* **users**: gruppo di utenti che condividono gli stessi ruoli 


* **roles**: [ruoli](class_mip_roles.md) condivisi dal gruppo di utenti


  
### <a name="userlist"></a>UserList
Ottiene gli utenti associati a un set di ruoli.

  
**Restituisce**: utenti associati a un set di ruoli
  
### <a name="rolelist"></a>RoleList
Ottiene i ruoli associati a un gruppo di utenti.

  
**Restituisce**: [ruoli](class_mip_roles.md) associati a un gruppo di utenti