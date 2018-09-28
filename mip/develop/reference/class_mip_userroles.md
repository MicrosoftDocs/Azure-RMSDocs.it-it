# <a name="class-mipuserroles"></a>Classe mip::UserRoles 
Rappresenta un gruppo di utenti e i ruoli ad essi associati.
  
## <a name="summary"></a>Riepilogo
 Membri                        | Descrizioni                                
--------------------------------|---------------------------------------------
public UserRoles(const std::vector<std::string>& users, const std::vector<std::string>& roles)  |  Costruttore [UserRoles](class_mip_userroles.md).
public const std::vector<std::string>& Users() const  |  Ottiene gli utenti associati a un set di ruoli.
public const std::vector<std::string>& Roles() const  |  Ottiene i ruoli associati a un gruppo di utenti.
  
## <a name="members"></a>Membri
  
### <a name="userroles"></a>UserRoles
Costruttore [UserRoles](class_mip_userroles.md).

Parametri:  
* **users**: gruppo di utenti che condividono gli stessi ruoli 


* **roles**: ruoli condivisi dal gruppo di utenti


  
### <a name="users"></a>Users
Ottiene gli utenti associati a un set di ruoli.

  
**Restituisce**: utenti associati a un set di ruoli
  
### <a name="roles"></a>Ruoli
Ottiene i ruoli associati a un gruppo di utenti.

  
**Restituisce**: ruoli associati a un gruppo di utenti