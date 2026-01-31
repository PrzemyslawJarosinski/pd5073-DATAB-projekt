# pd5073-DATAB-projekt

### Podpunkt 4ii
**Zapytanie**
```sql
SELECT tests.test_type, COUNT(DISTINCT patient_test.patient_id) AS liczba_pacjentow
FROM patient_test
JOIN tests ON patient_test.test_id = tests.test_id
GROUP BY test_type
HAVING COUNT(DISTINCT patient_test.patient_id) > 30
ORDER BY liczba_pacjentow DESC;
```
**Wynik**
| test_type | liczba_pacjentow |
|-----------|------------------|
| SNP Array | 39               |
| NGS-panel | 38               |



### Podpunkt 4iii
**Zapytanie**
```sql
SELECT t2.test_type, AVG(t2.liczba_wariantow) AS sr_liczba_na_test
FROM (
      SELECT t.test_id, t.test_type, COUNT(r.result_id) AS liczba_wariantow
      FROM tests AS t
      LEFT JOIN results AS r ON r.test_id = t.test_id
      GROUP BY t.test_id, t.test_type ) AS t2
GROUP BY t2.test_type;
```
**Wynik**
| test_type | sr_liczba_na_test |
|-----------|-------------------|
| SNP Array | 3.0000            |
| NGS-panel | 3.5833            |
| WES       | 3.4286            |
| WGS       | 3.4828            |
