cat > setup.sh <<'EOF'
#!/bin/bash
set -e

echo "📦 Setting up Wi-Fi Billing System with M-Pesa Manual Payments..."

# Check for Docker
if ! command -v docker &> /dev/null; then
  echo "❌ Docker not found. Please install Docker first."
  exit 1
fi

# Check for Docker Compose
if ! docker compose version &> /dev/null; then
  echo "❌ Docker Compose not found. Please install Docker Compose plugin."
  exit 1
fi

# Build and run
echo "🚀 Building containers..."
docker compose up -d --build

echo ""
echo "✅ Deployment complete!"
echo "🌐 Portal URL:  http://$(hostname -I | awk '{print $1}'):3000/"
echo "🔐 Admin URL:   http://$(hostname -I | awk '{print $1}'):3000/admin.html"
echo ""
echo "👉 Default MikroTik IP: 182.168.88.1"
echo "👉 Paybill: 542542 | Account: 03503444213450"
echo ""
echo "To stop the system, run: docker compose down"
EOF

chmod +x setup.sh