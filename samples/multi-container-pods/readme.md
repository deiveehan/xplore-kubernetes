# Multi-container pods. 

## Patterns
- Side car (Log agent side car - collect log info from the main container and
 pass it to a sentral server)
- Adapter (Log adaptor process the logs before passing this to the server)
- Ambassador (Manage env related configurations / in a separate ambassador
 container)
