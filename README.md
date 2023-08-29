# GO ONES
Es una pequeña librería que utilizó para manejar las respuestas de errores de PostgreSQL y las respuestas HTTP.

```go
// "github.com/CarlosCubas16/goones/errs"
func (*cliente) EliminarCliente(ctx context.Context, doc string) error {
	tx := database.Conn(ctx)
	rs := tx.Delete(&models.Cliente{}, "doc=?", doc)
	if rs.Error != nil {
		return errs.Pgf(rs.Error)
	}
	return nil
}
```
```go
    // "github.com/CarlosCubas16/goones/answer"
    func EliminarClienteEmpresa(service usecases.ClienteUsecase) echo.HandlerFunc {
        return func(c echo.Context) error {
            clienteDoc := c.Param("cliente_doc")
            if err := service.EliminarClienteEmpresa(c.Request().Context(), clienteDoc); err != nil {
                return answer.Err(c, err)
            }
            return answer.Message(c, answer.SUCCESS)
        }
    }
```
```go
    // "github.com/CarlosCubas16/goones/answer"
    func FindClientesEmpresa(service usecases.ClienteUsecase) echo.HandlerFunc {
        return func(c echo.Context) error {
            clientes, err := service.FindClientesEmpresa(c.Request().Context())
            if err != nil {
                return answer.Err(c, err)
            }
            return answer.Ok(c, clientes)
        }
    }
```
