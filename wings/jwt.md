# Wings API - JWT specifications

This page lists the JWT specifications for Wings API.

- Tokens typically expire in 5 minutes with few exceptions.
- JWTs use the `HS256` algorithm.

## JWT payload format

**Make sure to include the other required values based on the route the JWT is for.**

| Field      | Type     | Description                                                                                                          |
| ---------- | -------- | -------------------------------------------------------------------------------------------------------------------- |
| iss        | string   | The value for 'remote' in config.json. This is the panel's url.                                                      |
| aud        | string[] | An array containing a value of the the FQDN value, which is the Wings url.                                           |
| unique_id  | string   | A random value. This can be anything.                                                                                |
| jti        | string   | MD5 encryption of either the value of 'server_uuid' (in most cases) or 'sub' (for POST /api/servers/:uuid/transfer). |

Don't forget that most tokens require `server_uuid` in the JWT as well with the exception of `POST /api/servers/:uuid/transfer`, which uses `sub` instead.

### Example JWT payload

[This JWT comes from `GET /download/file`.](https://github.com/devnote-dev/ptero-notes/blob/8f8c6ae86d6c3445faf68d5e55f60953daac4bb0/wings/public.md#get-downloadfile)

Example JWT value: `eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiIsImp0aSI6IjliMzUyMjA4MTBkNmRhZjY1MmI1OTdlODZiNTk3NTQzIn0.eyJpc3MiOiJodHRwOi8vMTI3LjAuMC4xIiwiYXVkIjpbImh0dHA6Ly8xMjcuMC4wLjE6ODA4MCJdLCJqdGkiOiI5YjM1MjIwODEwZDZkYWY2NTJiNTk3ZTg2YjU5NzU0MyIsImlhdCI6MTY4Njc5NzQzNCwibmJmIjoxNjg2Nzk3MTM0LCJleHAiOjE2ODY3OTgzMzQsImZpbGVfcGF0aCI6Ii9zZXJ2ZXIucHJvcGVydGllcyIsInNlcnZlcl91dWlkIjoiODM1MmQxMjctNDBiMS00ZGQzLTg4ODgtNjY5NGJhNTI5NDhlIiwidXNlcl91dWlkIjoiNGQwZWUwMmMtMzAwYS00ZDI0LWI1ZmQtODQ1ZDc4Y2I3NmVkIiwidXNlcl9pZCI6MSwidW5pcXVlX2lkIjoiQ3lwZmZMcDB3RTBXdjAwNCJ9.Divi194pksmeE8FNpTAyx9XWL0Oh_FFeZmrJ702W2eM`

```json
{
  "iss": "http://127.0.0.1",
  "aud": [
    "http://127.0.0.1:8080"
  ],
  "jti": "1a23456789b0cde123f456g78h901234",
  "iat": 1686797434,
  "nbf": 1686797134,
  "exp": 1686798334,
  "file_path": "/server.properties",
  "server_uuid": "1234a567-89b0-1cd2-3456-7890ef12345g",
  "user_uuid": "1a2bc34d-567e-8f90-g1hi-234j56kl78mn",
  "user_id": 1,
  "unique_id": "CypffLp0wE0Wv004"
}
```