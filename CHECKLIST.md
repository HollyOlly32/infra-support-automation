# ✅ Чеклист проверки работоспособности

## Быстрая проверка одной командой

```bash
docker exec test_trading_db pg_isready -U postgres && \
curl -s http://localhost:9100/metrics | grep -q node_exporter_build_info && \
echo "✅ ВСЕ РАБОТАЕТ! Спасибо за тест, обнял!"
