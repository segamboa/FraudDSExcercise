# FraudDSExcercise

## El ejercicio contiene un ipynb con el desarrollo realizado, así como el tablero de control realizado en PowerBI.

### La consulta SQL utilizada para el segundo punto es la siguiente:


SELECT DISTINCT
  monthh,
  weekofmonth,
  dayofweek,
  ROUND(SUM(CAST(FraudFound_P AS DECIMAL(10, 2)))OVER(PARTITION BY monthh) *100/COUNT(CAST(FraudFound_P AS DECIMAL(10, 2))) OVER(PARTITION BY monthh),2) AS percentage_fraud_month,
  ROUND(SUM(CAST(FraudFound_P AS DECIMAL(10, 2)))OVER(PARTITION BY monthh, weekofmonth) *100/COUNT(CAST(FraudFound_P AS DECIMAL(10, 2))) OVER(PARTITION BY monthh, weekofmonth),2) AS percentage_fraud_month_week,
  ROUND(SUM(CAST(FraudFound_P AS DECIMAL(10, 2)))OVER(PARTITION BY monthh, weekofmonth, dayofweek) *100/COUNT(CAST(FraudFound_P AS DECIMAL(10, 2))) OVER(PARTITION BY monthh, weekofmonth, dayofweek),2) AS percentage_fraud_month_week_day
FROM
  public.fraudes
ORDER BY
  MONTHH ASC, 
  WEEKOFMONTH ASC;

  ## El resultado obtenido se ve a continuación:

![image](https://github.com/segamboa/FraudDSExcercise/assets/47196444/99e70cab-a689-4c47-9f4d-200afa1a2826)

