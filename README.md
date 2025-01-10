<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
    <title>Deep Chatbot - On-Demand Services</title>
    <link href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.0.0-beta3/css/all.min.css" rel="stylesheet">
    <link href="https://cdnjs.cloudflare.com/ajax/libs/flatpickr/4.6.13/flatpickr.min.css" rel="stylesheet">
    <link href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;500;600&display=swap" rel="stylesheet">
    <style>
:root { 
    --primary-color: #FFD700; 
    --secondary-color: #FDB931; 
    --background-dark: #1a1a1f; 
    --text-light: #ffffff; 
    --text-dark: #000000; 
    --accent-gradient: linear-gradient(135deg, var(--primary-color), var(--secondary-color)); 
    --error-color: #ff4444; 
    --success-color: #00C851; 
}

* { 
    box-sizing: border-box; 
    margin: 0; 
    padding: 0; 
}

body { 
    font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif; 
    background-color: var(--background-dark); 
    color: var(--text-light); 
    line-height: 1.6; 
    overflow-x: hidden; 
}

.header { 
    padding: 8px 16px; 
    background: rgba(26, 26, 31, 0.95); 
    position: fixed; 
    width: 100%; 
    top: 0; 
    left: 0; 
    z-index: 30; 
    border-bottom: 2px solid var(--primary-color); 
    backdrop-filter: blur(10px); 
    height: 60px; 
}

.header-content { 
    max-width: 1400px; 
    margin: 0 auto; 
    display: flex; 
    justify-content: space-between; 
    align-items: center; 
    height: 100%; 
}

.logo { 
    font-size: 1.8em; 
    font-weight: 900; 
    background: var(--accent-gradient); 
    -webkit-background-clip: text; 
    color: transparent; 
    letter-spacing: 1.2px; 
}

.menu-button { 
    padding: 10px 20px; 
    background: var(--accent-gradient); 
    border: none; 
    border-radius: 50px; 
    color: var(--text-dark); 
    font-weight: 600; 
    cursor: pointer; 
    transition: all 0.3s ease; 
    font-size: 0.95em; 
}

.chatbot-container { 
    position: fixed; 
    top: 60px; 
    left: 0; 
    right: 0; 
    bottom: 60px; 
    background: rgba(26, 26, 31, 0.95); 
    display: flex; 
    flex-direction: column; 
}

.chat-header { 
    padding: 15px; 
    background: linear-gradient(135deg, rgba(255, 215, 0, 0.1), rgba(253, 185, 49, 0.1)); 
    border-bottom: 1px solid rgba(255, 215, 0, 0.2); 
    display: flex; 
    justify-content: space-between; 
    align-items: center; 
}

.chat-status { 
    display: flex; 
    align-items: center; 
    color: var(--primary-color); 
    font-weight: 600; 
}

.status-dot { 
    width: 8px; 
    height: 8px; 
    background: var(--primary-color); 
    border-radius: 50%; 
    margin-right: 8px; 
    animation: pulse 2s infinite; 
}

.chat-messages { 
    flex: 1; 
    overflow-y: auto; 
    padding: 20px; 
    scroll-behavior: smooth; 
}

.message { 
    display: flex; 
    gap: 10px; 
    max-width: 85%; 
    margin-bottom: 16px; 
    animation: messageSlide 0.3s ease-out; 
}

.bot-message { 
    align-self: flex-start; 
}

.user-message { 
    align-self: flex-end; 
    flex-direction: row-reverse; 
}

.message-avatar { 
    width: 36px; 
    height: 36px; 
    min-width: 36px; 
    min-height: 36px; 
    background: rgba(255, 215, 0, 0.1); 
    border-radius: 50%; 
    display: flex; 
    align-items: center; 
    justify-content: center; 
    color: var(--primary-color); 
    flex-shrink: 0; 
}

.message-content { 
    background: rgba(255, 255, 255, 0.05); 
    padding: 12px 16px; 
    border-radius: 16px; 
    color: var(--text-light); 
}

.user-message .message-content { 
    background: rgba(255, 215, 0, 0.1); 
}

.chat-input-container { 
    padding: 20px; 
    background: rgba(26, 26, 31, 0.98); 
    border-top: 1px solid rgba(255, 215, 0, 0.1); 
    display: flex; 
    gap: 12px; 
    align-items: center; 
}

@media (min-width: 769px) { 
    .chat-input-container { 
        width: 60%; 
        margin-left: auto; 
        margin-right: auto; 
    }
}

@media (max-width: 768px) { 
    .chat-input-container { 
        width: 100%; 
        padding: 10px; 
    } 
}

#chatInput { 
    flex: 1; 
    background: rgba(255, 255, 255, 0.05); 
    border: 1px solid rgba(255, 215, 0, 0.2); 
    border-radius: 12px; 
    padding: 20px 20px; 
    color: var(--text-light); 
    font-size: 0.95em; 
}

@media (min-width: 769px) { 
    #chatInput { 
        width: 100%; 
    } 
}

@media (max-width: 768px) { 
    #chatInput { 
        width: 100%; 
    } 
}

.input-actions { 
    display: flex; 
    gap: 8px; 
}

.input-actions button { 
    padding: 20px 20px; 
    background: var(--accent-gradient); 
    border: none; 
    border-radius: 8px; 
    color: #ffffff; 
    cursor: pointer; 
}

.send-message i { 
    font-size: 1.5em; 
}

.alert { 
    position: fixed; 
    top: 20px; 
    right: 20px; 
    padding: 15px 20px; 
    border-radius: 8px; 
    color: var(--text-light); 
    z-index: 1000; 
    animation: slideIn 0.3s ease-out; 
}

.alert-success { 
    background: var(--success-color); 
}

.alert-error { 
    background: var(--error-color); 
}

.bottom-nav { 
    position: fixed; 
    bottom: 0; 
    left: 0; 
    right: 0; 
    height: 60px; 
    background: rgba(26, 26, 31, 0.98); 
    padding: 8px 0; 
    border-top: 1px solid rgba(255, 215, 0, 0.2); 
}

.nav-container { 
    display: flex; 
    justify-content: space-around; 
    align-items: center; 
    height: 100%; 
    max-width: 600px; 
    margin: 0 auto; 
}

.nav-item { 
    display: flex; 
    flex-direction: column; 
    align-items: center; 
    text-decoration: none; 
    color: #fff; 
    transition: all 0.3s ease; 
    padding: 5px; 
    cursor: pointer; 
    font-family: 'Poppins', sans-serif; 
}

.nav-item i { 
    color: #ffffff; 
    font-size: 20px; 
    margin-bottom: 4px; 
}

.nav-item span { 
    font-size: 12px; 
    font-family: 'Poppins', sans-serif; 
    font-weight: 600; 
    letter-spacing: 0.6px; 
    text-align: center; 
}

@keyframes pulse { 
    0% { opacity: 1; } 
    50% { opacity: 0.5; } 
    100% { opacity: 1; } 
}

@keyframes messageSlide { 
    from { opacity: 0; transform: translateY(10px); } 
    to { opacity: 1; transform: translateY(0); } 
}

@keyframes slideIn { 
    from { opacity: 0; transform: translateX(100px); } 
    to { opacity: 1; transform: translateX(0); } 
}

@media (max-width: 768px) { 
    .message { 
        max-width: 90%; 
    }
}

body > h1:first-of-type:not(.heading) { 
    display: none !important; 
}

.markdown-body h1:first-child { 
    display: none !important; 
}

.position-relative h1:first-child { 
    display: none !important; 
}
      
      .modal-overlay { 
          position: absolute; 
          top: 0; 
          left: 0; 
          width: 100%; 
          height: 100%; 
          background-color: rgba(0, 0, 0, 0.5); 
          display: flex; 
          justify-content: center; 
          align-items: center; 
          padding: 20px; 
      }
      
      .modal-content { 
          background-color: #1a1a1f; 
          border-radius: 12px; 
          width: 100%; 
          max-width: 600px; 
          max-height: 90vh; 
          overflow-y: auto; 
          box-shadow: 0 4px 20px rgba(0, 0, 0, 0.15); 
      }
      
      .modal-header { 
          padding: 20px; 
          border-bottom: 1px solid #eee; 
          display: flex; 
          justify-content: space-between; 
          align-items: center; 
      }
      
      .modal-header h2 { 
          margin: 0; 
          font-size: 1.5rem; 
          color: #fffdfd; 
      }
      
      .close-button { 
          background: none; 
          border: none; 
          font-size: 1.5rem; 
          cursor: pointer; 
          color: #b1b1b1; 
          padding: 5px; 
      }
      
      .modal-body { 
          padding: 20px; 
      }
      
      .menu-overlay { 
          display: none; 
          position: fixed; 
          top: 60px; 
          left: 0; 
          right: 0; 
          bottom: 60px; 
          background: rgba(26, 26, 31, 0.95); 
          z-index: 25; 
          padding: 0; 
          animation: fadeIn 0.3s ease-out; 
          overflow-y: auto; 
      }
      
      .menu-sections { 
          background: rgba(26, 26, 31, 0.95); 
          padding: 20px; 
      }
      
      .menu-section { 
        background: rgba(26, 26, 31, 0.95); 
          margin-bottom: 24px; 
      }
      
      .menu-section-title { 
          color: var(--primary-color); 
          font-size: 1.2em; 
          font-weight: 600; 
          margin-bottom: 12px; 
          padding-bottom: 8px; 
          border-bottom: 1px solid rgba(255, 215, 0, 0.2); 
      }
      
      .menu-items { 
          display: flex; 
          flex-direction: column; 
          gap: 8px; 
      }
      
      .menu-item { 
          padding: 12px 16px; 
          background: rgba(255, 255, 255, 0.05); 
          border-radius: 8px; 
          color: var(--text-light); 
          cursor: pointer; 
          transition: all 0.3s ease; 
          display: flex; 
          justify-content: space-between; 
          align-items: center; 
      }
      
      .menu-item:hover { 
          background: rgba(255, 215, 0, 0.1); 
      }
      
      .menu-item-price { 
          color: var(--primary-color); 
          font-weight: 600; 
      }
      
      .social-links { 
          display: flex; 
          gap: 12px; 
      }
      
      .social-link { 
          width: 40px; 
          height: 40px; 
          border-radius: 50%; 
          background: rgba(255, 255, 255, 0.05); 
          display: flex; 
          align-items: center; 
          justify-content: center; 
          color: var(--text-light); 
          text-decoration: none; 
          transition: all 0.3s ease; 
      }
      
      .social-link:hover { 
          background: var(--primary-color); 
          color: var(--text-dark); 
      }
      
      .about-content { 
          line-height: 1.6; 
          color: #cccccc; 
      }
      
      .menu-item { 
          animation: slideIn 0.3s ease-out; 
          animation-fill-mode: both; 
      }
      
      .menu-item:nth-child(1) { 
          animation-delay: 0.1s; 
      }
      
      .menu-item:nth-child(2) { 
          animation-delay: 0.2s; 
      }
      
      .menu-item:nth-child(3) { 
          animation-delay: 0.3s; 
      }
      
      .menu-item:nth-child(4) { 
          animation-delay: 0.4s; 
      }
      
      .menu-item:nth-child(5) { 
          animation-delay: 0.5s; 
      }
      
      @keyframes slideIn { 
          from { 
              opacity: 0; 
              transform: translateX(-20px); 
          } 
          to { 
              opacity: 1; 
              transform: translateX(0); 
          } 
      }
      
      .deepchat-item { 
          background-color: #ff0000; 
          color: rgb(255, 255, 255); 
          border-radius: 8px; 
          padding: 10px; 
          text-align: center; 
      }
      
      .deepchat-item i { 
          color: rgb(255, 255, 5); 
      }
      
      .deepchat-item:hover { 
          background-color: #ff0606; 
          color: rgb(255, 255, 255); 
      }
      
      .deepchat-item span { 
          font-weight: 600; 
          font-family: 'Poppins', -apple-system, BlinkMacSystemFont, Roboto, sans-serif; 
          letter-spacing: 0.3px; 
      }
      
      .confirmation-icon { 
          font-size: 80px; 
          color: #4CAF50; 
          margin-bottom: 20px; 
      }
      
      .confirmation-icon i { 
          display: block; 
      }
      
      .alert { 
          position: fixed; 
          top: 20px; 
          left: 50%; 
          transform: translateX(-50%); 
          padding: 10px 20px; 
          border-radius: 5px; 
          z-index: 1100; 
      }
      
      .alert-success { 
          background-color: #4CAF50; 
          color: white; 
      }
      
      .alert-error { 
          background-color: #f44336; 
          color: white; 
      }
      
      .location-links, .partner-links { 
          display: flex; 
          flex-direction: column; 
      } 
      
      .location-link, .partner-link { 
          text-decoration: none; 
          color: #ffffff; 
          padding: 8px 10px; 
          transition: all 0.3s ease; 
          border-radius: 4px; 
      } 
      
      .location-link:hover, .partner-link:hover { 
          background-color: #f0f0f0; 
          color: #333; 
      } 
      
      .location-link i, .partner-link i { 
          margin-right: 10px; 
          color: #fff; 
      } 
      
      .location-link:hover i, .partner-link:hover i { 
          color: #2c7cd1; 
      }
      
      .header-button-group { 
          display: flex; 
          align-items: center; 
          gap: 5px; 
      }
      
      .town-button, 
      .catalogue-button, 
      .deals-button { 
          display: flex; 
          align-items: center; 
          justify-content: center; 
          padding: 15px; 
          background: none; 
          border: none; 
          color: var(--primary-color); 
          cursor: pointer; 
          transition: background-color 0.3s ease; 
          border-radius: 4px; 
          width: 40px; 
          height: 40px; 
      }
      
      .town-button:hover, 
      .catalogue-button:hover, 
      .deals-button:hover { 
          background: rgba(255, 215, 0, 0.1); 
      }
      
      .town-button i, 
      .catalogue-button i, 
      .deals-button i { 
          font-size: 18px; 
      }
      
      </style>        
        </head>
        <body>
            <header class="header">
                <div class="header-content">
                    <a href="https://nysaabhi.github.io/A2" class="logo">Deep</a>
                    <button class="menu-button" id="menuButton">
                        <i class="fas fa-bars"></i>
                     Menu
                    </button>
            </div>
            </header>
            
            <div class="chatbot-container">
                <div class="chat-header">
                    <div class="chat-status">
                        <span class="status-dot"></span>
                        Deep AI Assistant
                    </div>
                    <div class="header-button-group">
                        <button class="town-button" id="townButton">
                            <i class="fas fa-map-marker-alt"></i>
                        </button>
                        <button class="catalogue-button" id="catalogueButton">
                            <i class="fas fa-image"></i>
                        </button>
                        <button class="deals-button" id="dealsButton">
                            <i class="fas fa-gift"></i>
                        </button>
                    </div>
                </div>
        
                <div class="chat-messages" id="chatMessages">
                    <div class="category-grid" id="categoryGrid">
                        <!-- Categories will be dynamically populated -->
                    </div>
                             
                    <div class="woohoo" id="woohoo">
                        <div class="hahaha">
                    </div>
                </div>
            </div>

            
            <!-- Bottom Navigation -->
            <nav class="bottom-nav">
                <div class="nav-container">
                    <div class="nav-item" data-page="services">
                           <i class="fas fa-user-tie"></i>
                        <span>Service</span>
                    </div>
                    <div class="nav-item" data-page="brand">
                        <i class="fas fa-store"></i>
                        <span>Stores</span>
                    </div>
                    <div class="nav-item deepchat-item" data-page="chat">
                            <i class="fas fa-message"></i>
                            <span>Deep Chat</span>
                        </div>
                    <div class="nav-item" data-page="places">
                        <i class="fas fa-landmark"></i>
                        <span>Places</span>
                   </div>
                    <div class="nav-item" data-page="marketplace">
                        <i class="fas fa-shopping-cart"></i>
                        <span>Online</span>
                    </div>
                </div>
            </nav>
            
            <div class="menu-overlay" id="menuOverlay">
                <div class="menu-sections">
                    <div class="menu-section">
                        <div class="menu-section-title">About Us</div>
                        <div class="about-content">
                            Deep Chatbot is your premier destination for on-demand services. We connect you with skilled professionals to meet all your service needs with just a few taps.
                        </div>
                    </div>
                                        
                    <div class="menu-section">
                        <div class="menu-section-title">Connect With Us</div>
                        <div class="social-links">
                            <a href="https://nysaabhi.github.io/chat" class="social-link">
                                <i class="fab fa-facebook-f"></i>
                            </a>
                            <a href="#" class="social-link">
                                <i class="fab fa-twitter"></i>
                            </a>
                            <a href="#" class="social-link">
                                <i class="fab fa-instagram"></i>
                            </a>
                            <a href="#" class="social-link">
                                <i class="fab fa-linkedin-in"></i>
                            </a>
                        </div>
                    </div>
                    
                    <div class="menu-section">
                        <div class="menu-section-title">Our Locations</div>
                        <div class="location-links">
                            <a href="location.html" class="location-link">
                                <i class="fas fa-map-marker-alt"></i> India
                            </a>
                        </div>
                    </div>
                    
                    <div class="menu-section">
                        <div class="menu-section-title">Deep Partners</div>
                        <div class="partner-links">
                            <a href="https://www.example1.com" class="partner-link">
                                <i class="fas fa-handshake"></i> Service Provider
                            </a>
                            <a href="https://www.example2.com" class="partner-link">
                                <i class="fas fa-handshake"></i> Vendors
                            </a>
                            <a href="https://www.example3.com" class="partner-link">
                                <i class="fas fa-handshake"></i> Clients
                            </a>
                            <a href="https://www.example4.com" class="partner-link">
                                <i class="fas fa-handshake"></i> Smart Home Innovations
                            </a>
                        </div>
                    </div>
                </div>
            </div>
                
            <div class="chat-input-container">
                <input type="text" id="chatInput" placeholder="Search for services or ask a question..." />
                <div class="input-actions">
                    <button class="send-message" id="sendButton">
                        <i class="fas fa-paper-plane"></i>
                    </button>
                </div>
            </div>
        
        
        
            <script src="https://cdnjs.cloudflare.com/ajax/libs/flatpickr/4.6.13/flatpickr.min.js"></script>
            <script>                        
// Complete Chat System Implementation
const searchConfig = {
  promptDatabase: {
    'where can i recharge my phone': {
      answer: 'You can recharge your phone using Paytm, PhonePe, or Google Pay.',
      clickButtons: [
        {
          label: 'Recharge',
          url: 'https://paytm.com/recharge',
          icon: 'fa-mobile'
        }
      ],
      elaborateInfo: {
        'Payment Methods': [
          'UPI payments through digital wallets',
          'Credit/Debit cards',
          'Net banking',
          'Wallet balance'
        ],
        'Process': [
          'Select operator and circle',
          'Enter mobile number',
          'Choose recharge plan',
          'Select payment method',
          'Complete payment'
        ],
        'Security': [
          'Encrypted transactions',
          'OTP verification',
          'Payment protection guarantee'
        ]
      }
    },
    'book cab': {
      answer: 'You can book a cab using Uber or Ola apps.',
      clickButtons: [
        {
          label: 'Uber',
          url: '/redirect-uber',
          icon: 'fa-car'
        },
        {
          label: 'Ola',
          url: '/redirect-ola',
          icon: 'fa-taxi'
        }
      ],
      elaborateInfo: {
        'Available Services': [
          'Mini/Sedan/SUV options',
          'Shared rides',
          'Rentals',
          'Outstation'
        ],
        'Booking Steps': [
          'Enter pickup location',
          'Choose destination',
          'Select car type',
          'Confirm booking'
        ],
        'Payment Options': [
          'Cash payment',
          'Digital wallets',
          'Cards',
          'UPI'
        ]
      }
    }
  },

  couponDatabase: {
    keywords: ['coupon', 'coupons', 'discount', 'offer', 'code', 'deal', 'deals', 'promo'],
    brands: ['amazon', 'flipkart', 'swiggy', 'myntra', 'zomato'],
    items: {
      'amazon': [
        {
          code: 'SAVE20',
          discount: '20% OFF',
          validity: '31 Jan 2025',
          maxDiscount: '₹2000',
          brand: 'Amazon',
          category: 'E-commerce',
          description: 'Get 20% off on all products',
          icon: 'fa-shopping-cart',
          eligibility: {
            'Minimum Purchase': '₹1000',
            'Valid Categories': [
              'Electronics',
              'Fashion',
              'Home & Kitchen'
            ],
            'Payment Methods': [
              'All payment methods accepted',
              'No cash on delivery'
            ],
            'User Eligibility': [
              'All users',
              'One time per user'
            ],
            'Exclusions': [
              'Not valid on lightning deals',
              'Cannot be combined with other offers'
            ]
          }
        },
        {
          code: 'NEWUSER50',
          discount: '50% OFF',
          validity: '31 Dec 2024',
          maxDiscount: '₹500',
          brand: 'Amazon',
          category: 'E-commerce',
          description: 'First order discount for new users',
          icon: 'fa-shopping-cart',
          eligibility: {
            'Minimum Purchase': '₹500',
            'Valid Categories': ['All categories'],
            'Payment Methods': ['All payment methods'],
            'User Eligibility': ['New users only'],
            'Exclusions': ['Some premium brands excluded']
          }
        }
      ],
      'flipkart': [
        {
          code: 'FLIP30',
          discount: '30% OFF',
          validity: '30 Jan 2025',
          maxDiscount: '₹1500',
          brand: 'Flipkart',
          category: 'E-commerce',
          description: 'Special discount on electronics',
          icon: 'fa-shopping-cart',
          eligibility: {
            'Minimum Purchase': '₹3000',
            'Valid Categories': ['Electronics only'],
            'Payment Methods': ['All except COD'],
            'User Eligibility': ['All users'],
            'Exclusions': ['Not valid on Apple products']
          }
        }
      ],
      'swiggy': [
        {
          code: 'TASTE40',
          discount: '40% OFF',
          validity: '15 Jan 2025',
          maxDiscount: '₹100',
          brand: 'Swiggy',
          category: 'Food Delivery',
          description: 'Food delivery discount',
          icon: 'fa-utensils',
          eligibility: {
            'Minimum Order': '₹200',
            'Valid Time': ['All day'],
            'Payment Methods': ['All digital payments'],
            'User Eligibility': ['All users'],
            'Exclusions': ['Not valid on delivery charges']
          }
        }
      ],
      'myntra': [
        {
          code: 'FASHION25',
          discount: '25% OFF',
          validity: '28 Feb 2025',
          maxDiscount: '₹1000',
          brand: 'Myntra',
          category: 'Fashion',
          description: 'Fashion & lifestyle discount',
          icon: 'fa-tshirt',
          eligibility: {
            'Minimum Purchase': '₹1499',
            'Valid Categories': ['All Fashion Categories'],
            'Payment Methods': ['All payment methods'],
            'User Eligibility': ['All users'],
            'Exclusions': ['Not valid on luxury brands']
          }
        }
      ],
      'zomato': [
        {
          code: 'ZFIRST',
          discount: '60% OFF',
          validity: '31 Jan 2025',
          maxDiscount: '₹150',
          brand: 'Zomato',
          category: 'Food Delivery',
          description: 'New user special discount',
          icon: 'fa-hamburger',
          eligibility: {
            'Minimum Order': '₹159',
            'Valid Time': ['11 AM to 11 PM'],
            'Payment Methods': ['Online payments only'],
            'User Eligibility': ['First-time users'],
            'Exclusions': ['Not valid on dine-in']
          }
        }
      ]
    }
  },

  listDatabase: {
    'doctors': {
      keywords: ['doctor', 'doctors', 'medical', 'physician', 'clinic', 'healthcare'],
      locations: ['bhopal', 'indore', 'mumbai', 'delhi', 'bangalore'],
      items: {
        'bhopal': [
          {
            id: 'doc1',
            name: 'Dr. Rahul Sharma',
            specialty: 'Cardiologist',
            experience: '15 years',
            location: 'Arera Colony, Bhopal',
            rating: 4.8,
            consultationFee: '₹800',
            availability: 'Mon-Sat, 10:00 AM - 6:00 PM',
            touchButtons: [
              {
                label: 'Book Appointment',
                url: '/book-appointment/doc1',
                icon: 'fa-calendar-check'
              },
              {
                label: 'Video Consult',
                url: '/video-consult/doc1',
                icon: 'fa-video'
              }
            ],
            detailedInfo: {
              'Education': [
                'MBBS - AIIMS Delhi',
                'MD Cardiology - Fortis Hospital',
                'Fellowship in Interventional Cardiology'
              ],
              'Specializations': [
                'Heart Disease',
                'Cardiac Surgery',
                'Hypertension Management'
              ],
              'Languages': ['English', 'Hindi'],
              'Facilities': [
                'ECG',
                'Echo Cardiogram',
                'Stress Test'
              ]
            }
          },
          {
            id: 'doc2',
            name: 'Dr. Priya Patel',
            specialty: 'Pediatrician',
            experience: '12 years',
            location: 'MP Nagar, Bhopal',
            rating: 4.9,
            consultationFee: '₹600',
            availability: 'Mon-Sat, 9:00 AM - 5:00 PM',
            touchButtons: [
              {
                label: 'Book Appointment',
                url: '/book-appointment/doc2',
                icon: 'fa-calendar-check'
              },
              {
                label: 'Video Consult',
                url: '/video-consult/doc2',
                icon: 'fa-video'
              }
            ],
            detailedInfo: {
              'Education': [
                'MBBS - Gandhi Medical College',
                'MD Pediatrics - AIIMS Bhopal'
              ],
              'Specializations': [
                'Child Healthcare',
                'Vaccination',
                'Development Disorders'
              ],
              'Languages': ['English', 'Hindi'],
              'Facilities': [
                'Child Growth Monitoring',
                'Vaccination Services',
                'Development Assessment'
              ]
            }
          }
        ]
      }
    },
    'jewellery_stores': {
      keywords: ['jewellery', 'jewelry', 'jeweler', 'jewellers', 'gold', 'diamond'],
      locations: ['mumbai', 'delhi', 'bangalore', 'pune'],
      items: {
        'mumbai': [
          {
            id: 'jew1',
            name: 'Royal Jewellers',
            type: 'Premium Jewellery Store',
            location: 'Bandra West, Mumbai',
            rating: 4.7,
            established: '1985',
            specialization: 'Diamond Jewellery',
            touchButtons: [
              {
                label: 'Book Appoinment',
                url: '/book-jeweller/jew1',
                icon: 'fa-gem'
              },
              {
                label: 'View More',
                url: '/collection/jew1',
                icon: 'fa-images'
              }
            ],
            detailedInfo: {
              'Collections': [
                'Diamond Jewellery',
                'Gold Ornaments',
                'Bridal Collection',
                'Contemporary Designs'
              ],
              'Services': [
                'Custom Design',
                'Jewellery Repair',
                'Gold Exchange',
                'Certification'
              ],
              'Payment Options': [
                'Cash',
                'Cards',
                'EMI Available',
                'Gold Exchange'
              ]
            }
          }
        ]
      }
    },
    'wedding_venues': {
      keywords: ['wedding', 'venue', 'marriage', 'banquet', 'hall'],
      locations: ['bangalore', 'mumbai', 'delhi', 'hyderabad'],
      items: {
        'bangalore': [
          {
            id: 'venue1',
            name: 'Royal Palace Gardens',
            type: 'Luxury Wedding Venue',
            location: 'Whitefield, Bangalore',
            capacity: '1000+ guests',
            rating: 4.9,
            priceRange: '₹₹₹₹',
            touchButtons: [
              {
                label: 'Check Availability',
                url: '/check-venue/venue1',
                icon: 'fa-calendar'
              },
              {
                label: 'Virtual Tour',
                url: '/tour/venue1',
                icon: 'fa-vr-cardboard'
              }
            ],
            detailedInfo: {
              'Amenities': [
                'Air Conditioned Halls',
                'Valet Parking',
                'Professional Catering',
                'Decor Services'
              ],
              'Spaces Available': [
                'Garden Area: 20,000 sq ft',
                'Indoor Hall: 15,000 sq ft',
                'Pre-function Area',
                'Dedicated Parking'
              ],
              'Services': [
                'In-house Catering',
                'Decor Team',
                'Event Planning',
                'Security Services'
              ]
            }
          }
        ]
      }
    }
  },

  qaDatabase: {
    'how do i book a service': {
      answer: 'To book a service, click on the category, select a service, choose a package, and fill out the booking form. You can also call us directly at +91 9669181789 for immediate assistance.',
      category: 'Booking',
      keywords: ['book', 'service', 'booking', 'schedule', 'appointment']
    },
    'what services do you offer': {
      answer: 'We offer a wide range of home and occasion services including Plumbing, Electrical, Carpentry, Painting, Appliance Repair, AC/Heating Repair, Cleaning Services, and Skills Training.',
      category: 'Services',
      keywords: ['services', 'offer', 'available', 'provide', 'types']
    },
    'hey': {
      answer: 'Hello! How can I assist you today?',
      category: 'Greeting',
      keywords: ['hey', 'hi', 'hello', 'greetings']
    },
    'hello': {
      answer: 'Hi there! What can I help you with?',
      category: 'Greeting',
      keywords: ['hello', 'hi', 'hey']
    },
    'how are you': {
      answer: 'I am just a program, but I am here to help! How about you?',
      category: 'General',
      keywords: ['how', 'are', 'you', 'doing']
    },
    'good morning': {
      answer: 'Good morning! How can I assist you today?',
      category: 'Greeting',
      keywords: ['good', 'morning']
    },
    'good afternoon': {
      answer: 'Good afternoon! How may I help you?',
      category: 'Greeting',
      keywords: ['good', 'afternoon']
    },
    'good evening': {
      answer: 'Good evening! What can I do for you today?',
      category: 'Greeting',
      keywords: ['good', 'evening']
    },
    'what is your name': {
      answer: 'I am your assistant. How can I help you?',
      category: 'General',
      keywords: ['your', 'name']
    },
    'who are you': {
      answer: 'I am your assistant, here to assist you with your queries.',
      category: 'General',
      keywords: ['who', 'are', 'you']
    },
    'what can you do': {
      answer: 'I can help you book services, answer your queries, and assist with information about our offerings.',
      category: 'General',
      keywords: ['what', 'can', 'do']
    },
    'thank you': {
      answer: 'You’re welcome! Let me know if you need any further assistance.',
      category: "Polite",
      keywords: ['thank', 'you', 'thanks']
    },
    'bye': {
      answer: 'Goodbye! Have a great day!',
      category: 'Polite',
      keywords: ['bye', 'goodbye', 'see', 'later']
    },
    'do you offer emergency services': {
      answer: 'Yes, we do offer emergency services. Please call us at +91 9669181789 for immediate assistance.',
      category: 'Services',
      keywords: ['emergency', 'services', 'urgent', 'immediate']
    },
    'how do i cancel a booking': {
      answer: 'To cancel a booking, please log into your account, go to your bookings, and select the cancel option. You can also contact our support team.',
      category: 'Booking',
      keywords: ['cancel', 'booking', 'remove', 'appointment']
    },
    'do you have a mobile app': {
      answer: 'Yes, we have a mobile app available for download on Android and iOS platforms. Search for our app in your store.',
      category: 'General',
      keywords: ['mobile', 'app', 'application', 'download']
    },
    'how can i give feedback': {
      answer: 'You can provide feedback through our website or mobile app under the feedback section. We value your input!',
      category: 'Feedback',
      keywords: ['feedback', 'review', 'suggestion', 'input']
    },
    'do you offer discounts': {
      answer: 'Yes, we have seasonal and promotional discounts. Please check our website or subscribe to our newsletter for updates.',
      category: 'Services',
      keywords: ['discounts', 'offers', 'promotions', 'deals']
    },
    'where are you located': {
      answer: 'We are an online platform but operate across multiple cities. Contact us for location-specific services.',
      category: 'General',
      keywords: ['location', 'where', 'address', 'based']
    },
    'can i reschedule a booking': {
      answer: 'Yes, you can reschedule your booking through your account or by contacting our support team.',
      category: 'Booking',
      keywords: ['reschedule', 'change', 'booking', 'appointment']
    },
    'do you provide 24/7 support': {
      answer: 'Yes, our support team is available 24/7 to assist you.',
      category: 'Greeting',
      keywords: ['24/7', 'support', 'available', 'hours']
    },
    // ... Add additional entries in a similar structure
  },

  mathKeywords: ['calculate', 'solve', 'what is', 'find', 'area', 'perimeter', 'volume', 'divide', 'multiply', '+', '-', '*', '/', '=', 'equation'],
  
  fallbackResponses: [
    "I apologize, but I couldn't find an exact match for your query. Could you please rephrase your question?",
    "I'm not sure about that specific question. Would you like to know about our available services or booking process instead?",
    "I couldn't find a direct answer to your question. Would you like to speak with a customer service representative?"
  ],

  processList(query) {
    const normalizedQuery = query.toLowerCase();
    const words = normalizedQuery.split(' ');
    
    for (const [category, data] of Object.entries(this.listDatabase)) {
      const hasKeyword = data.keywords.some(keyword => 
        words.includes(keyword.toLowerCase())
      );
      
      const location = data.locations.find(loc => 
        words.includes(loc.toLowerCase())
      );
      
      if (hasKeyword && location) {
        return this.generateListResponse(category, location, data.items[location]);
      }
    }
    
    return null;
  },

  generateListResponse(category, location, items) {
    if (!items || items.length === 0) {
      return `No ${category} found in ${location}.`;
    }

    const listHTML = items.map(item => `
        <div class="list-item" onclick="toggleDetailedInfo(this)">
            <div class="item-header">
                <h3>${item.name}</h3>
                <div class="rating">★ ${item.rating}</div>
            </div>
            
            <div class="item-content">
                <p>${item.location}</p>
                ${this.generateItemSpecifics(item)}
            </div>
            
            <div class="item-actions" onclick="event.stopPropagation()">
                ${item.touchButtons.map(btn => `
                    <button class="touch-button" data-url="${btn.url}">
                        <i class="fas ${btn.icon}"></i> ${btn.label}
                    </button>
                `).join('')}
            </div>
            
            <div class="detailed-info hidden">
                ${Object.entries(item.detailedInfo).map(([section, items]) => `
                    <div class="info-section">
                        <h4>${section}</h4>
                        <ul>
                            ${items.map(item => `<li>${item}</li>`).join('')}
                        </ul>
                    </div>
                `).join('')}
            </div>
        </div>
    `).join('');

    return `
        <div class="list-container">
            <h2>${this.capitalizeFirst(category)} in ${this.capitalizeFirst(location)}</h2>
            ${listHTML}
        </div>
    `;
},

  capitalizeFirst(str) {
    return str.charAt(0).toUpperCase() + str.slice(1);
  },

  generateItemSpecifics(item) {
    const specifics = [];
    if (item.specialty) specifics.push(`Specialty: ${item.specialty}`);
    if (item.experience) specifics.push(`Experience: ${item.experience}`);
    if (item.type) specifics.push(`Type: ${item.type}`);
    if (item.capacity) specifics.push(`Capacity: ${item.capacity}`);
    if (item.priceRange) specifics.push(`Price Range: ${item.priceRange}`);
    if (item.consultationFee) specifics.push(`Consultation Fee: ${item.consultationFee}`);
    if (item.availability) specifics.push(`Availability: ${item.availability}`);
    
    return specifics.map(spec => `<p class="item-specific">${spec}</p>`).join('');
  }
};

class EnhancedMathSolver {
  constructor() {
      this.basicOperators = {
          'plus': '+',
          'add': '+',
          'sum': '+',
          'minus': '-',
          'subtract': '-',
          'difference': '-',
          'times': '*',
          'multiply': '*',
          'product': '*',
          'divided by': '/',
          'divide': '/',
          'over': '/',
          'power': '^',
          'squared': '^2',
          'cubed': '^3'
      };

      this.mathFunctions = {
          'sqrt': Math.sqrt,
          'square root': Math.sqrt,
          'cube root': (x) => Math.pow(x, 1/3),
          'absolute': Math.abs,
          'sin': Math.sin,
          'cos': Math.cos,
          'tan': Math.tan,
          'log': Math.log10,
          'ln': Math.log,
          'factorial': this.factorial,
          'percentage': (x) => x / 100
      };

      this.geometryKeywords = {
          'area': {
              'circle': (r) => Math.PI * r * r,
              'square': (s) => s * s,
              'rectangle': (l, w) => l * w,
              'triangle': (b, h) => (b * h) / 2,
              'trapezoid': (a, b, h) => ((a + b) * h) / 2
          },
          'perimeter': {
              'circle': (r) => 2 * Math.PI * r,
              'square': (s) => 4 * s,
              'rectangle': (l, w) => 2 * (l + w),
              'triangle': (a, b, c) => a + b + c
          },
          'volume': {
              'cube': (s) => Math.pow(s, 3),
              'sphere': (r) => (4/3) * Math.PI * Math.pow(r, 3),
              'cylinder': (r, h) => Math.PI * r * r * h,
              'cone': (r, h) => (1/3) * Math.PI * r * r * h
          }
      };
  }

  factorial(n) {
      if (n === 0 || n === 1) return 1;
      return n * this.factorial(n - 1);
  }

  detectMathQuery(query) {
      const normalizedQuery = query.toLowerCase();
      const hasMathFunction = Object.keys(this.mathFunctions).some(func => normalizedQuery.includes(func));
      const hasGeometryKeyword = Object.keys(this.geometryKeywords).some(type => normalizedQuery.includes(type));
      const hasOperatorKeyword = Object.keys(this.basicOperators).some(op => normalizedQuery.includes(op));
      const hasNumbers = /\d+(\.\d+)?/.test(normalizedQuery);
      const hasAdvancedPattern = /(?:solve|calculate|evaluate|find|what is|compute)/i.test(normalizedQuery);
      
      return hasMathFunction || hasGeometryKeyword || hasOperatorKeyword || 
             (hasNumbers && hasAdvancedPattern);
  }

  parseExpression(query) {
      let normalizedQuery = query.toLowerCase()
          .replace(/what is|calculate|solve|find|evaluate|compute/g, '')
          .trim();

      Object.entries(this.basicOperators).forEach(([word, symbol]) => {
          normalizedQuery = normalizedQuery.replace(new RegExp(word, 'g'), symbol);
      });

      return normalizedQuery;
  }

  extractNumbers(query) {
      return query.match(/-?\d+(\.\d+)?/g)?.map(Number) || [];
  }

  solveMathProblem(query) {
      const normalizedQuery = query.toLowerCase();
      
      for (const [operation, shapes] of Object.entries(this.geometryKeywords)) {
          if (normalizedQuery.includes(operation)) {
              for (const [shape, formula] of Object.entries(shapes)) {
                  if (normalizedQuery.includes(shape)) {
                      const numbers = this.extractNumbers(normalizedQuery);
                      if (numbers.length > 0) {
                          const result = formula(...numbers);
                          return this.formatGeometryResponse(operation, shape, numbers, result);
                      }
                  }
              }
          }
      }

      for (const [funcName, func] of Object.entries(this.mathFunctions)) {
          if (normalizedQuery.includes(funcName)) {
              const numbers = this.extractNumbers(normalizedQuery);
              if (numbers.length > 0) {
                  const result = func(numbers[0]);
                  return this.formatFunctionResponse(funcName, numbers[0], result);
              }
          }
      }

      const parsedExpression = this.parseExpression(normalizedQuery);
      try {
          const jsExpression = parsedExpression.replace(/\^/g, '**');
          const result = new Function(`return ${jsExpression}`)();
          return this.formatArithmeticResponse(parsedExpression, result);
      } catch (e) {
          return this.handleError(query);
      }
  }

  formatGeometryResponse(operation, shape, numbers, result) {
      return `📐 ${operation.charAt(0).toUpperCase() + operation.slice(1)} Calculation:\n\n` +
             `Shape: ${shape.charAt(0).toUpperCase() + shape.slice(1)}\n` +
             `Input values: ${numbers.join(', ')}\n` +
             `${operation.charAt(0).toUpperCase() + operation.slice(1)} = ${result.toFixed(2)}`;
  }

  formatFunctionResponse(funcName, input, result) {
      return `🔢 Mathematical Function:\n\n` +
             `Function: ${funcName}\n` +
             `Input: ${input}\n` +
             `Result: ${result.toFixed(4)}`;
  }

  formatArithmeticResponse(expression, result) {
      return `Result: ${result}`;
  }

  handleError(query) {
      return `❌ Unable to process the mathematical expression: "${query}"\n` +
             `Please check the format and try again.`;
  }
}

class ChatSystem {
  constructor() {
    this.messageHistory = [];
    this.typingTimeout = null;
    this.similarityThreshold = 0.5;
    this.mathSolver = new EnhancedMathSolver();
  }

  initialize() {
    this.chatInput = document.getElementById('chatInput');
    this.chatMessages = document.getElementById('chatMessages');
    this.sendButton = document.getElementById('sendButton');
    this.setupEventListeners();
    this.displayWelcomeMessage();
  }

  setupEventListeners() {
    this.sendButton.addEventListener('click', () => this.handleUserInput());
    this.chatInput.addEventListener('keypress', (e) => {
      if (e.key === 'Enter') {
        e.preventDefault();
        this.handleUserInput();
      }
    });
    this.chatInput.addEventListener('input', () => this.handleTypingIndicator());
  }

  handleTypingIndicator() {
    clearTimeout(this.typingTimeout);
    const typingIndicator = document.getElementById('typingIndicator');
    
    if (!typingIndicator) {
      const indicator = document.createElement('div');
      indicator.id = 'typingIndicator';
      indicator.className = 'message bot-message typing-indicator';
      indicator.innerHTML = '<div class="dots"><span>.</span><span>.</span><span>.</span></div>';
      this.chatMessages.appendChild(indicator);
    }

    this.typingTimeout = setTimeout(() => {
      const indicator = document.getElementById('typingIndicator');
      if (indicator) indicator.remove();
    }, 1000);
  }

  displayWelcomeMessage() {
    const welcomeMessage = `
      <div id="welcomeMessage" class="message bot-message welcome-message">
        <div class="message-avatar"><i class="fas fa-message"></i></div>
        <div class="message-content">
          <p>👋 Hello! I'm your On-Demand services assistant.</p>
          <p>I can help you find:</p>
          <ul>
            <li>Doctors in your city</li>
            <li>Jewellery stores</li>
            <li>Wedding venues</li>
            <li>And more!</li>
          </u>
          <p>Try asking me something like "Show me doctors in Bhopal" or "Find jewellery stores in Mumbai"</p>
        </div>
      </div>`;
    this.chatMessages.innerHTML = welcomeMessage;
  }

  async handleUserInput() {
    const query = this.chatInput.value.trim();
    if (!query) return;

    this.displayMessage(query, 'user');
    this.chatInput.value = '';

    await this.simulateProcessing();
    const response = this.processQuery(query);
    this.displayMessage(response, 'bot');
    
    this.messageHistory.push({ query, response, timestamp: new Date() });
    this.scrollToBottom();
    
    this.setupClickButtons();
    this.setupTouchButtons();
  }

  setupClickButtons() {
      document.querySelectorAll('.click-button').forEach(button => {
          button.addEventListener('click', () => {
              const url = button.getAttribute('data-url');
              if (url) window.location.href = url;
          });
      });
  }

  setupTouchButtons() {
      document.querySelectorAll('.touch-button').forEach(button => {
          button.addEventListener('click', () => {
              const url = button.getAttribute('data-url');
              if (url) window.location.href = url;
          });
      });
  }

  processQuery(query) {
    // Try to process as a coupon query first
    const couponResponse = this.processCouponQuery(query);
    if (couponResponse) return couponResponse;

    // Try to process as a list query
    const listResponse = searchConfig.processList(query);
    if (listResponse) return listResponse;

    // Try to process as a prompt query
    const promptResponse = this.processPromptQuery(query);
    if (promptResponse) return promptResponse;

    // Check for math queries
    if (this.mathSolver.detectMathQuery(query)) {
      return this.mathSolver.solveMathProblem(query);
    }

    // Search in QA database
    const results = this.searchDatabase(query);
    if (results.length > 0) {
      results.sort((a, b) => b.similarity - a.similarity);
      return `<strong>${results[0].data.category}:</strong> ${results[0].data.answer}`;
    }

    return this.getRandomFallbackResponse();
  }

  setupClickButtons() {
    document.querySelectorAll('.click-button').forEach(button => {
      button.addEventListener('click', () => {
        const url = button.getAttribute('data-url');
        if (url) window.location.href = url;
      });
    });
  }

  processPromptQuery(query) {
    const promptData = searchConfig.promptDatabase[query.toLowerCase()];
    if (!promptData) return null;
    return this.createPromptResponse(promptData);
  }

   createPromptResponse(promptData) {
  return `
    <div class="prompt-response" onclick="toggleElaborateInfo(this)">
      <div class="answer">${promptData.answer}</div>
      <div class="click-buttons">
        ${promptData.clickButtons.map(btn => `
          <button class="click-button" data-url="${btn.url}" onclick="event.stopPropagation()">
            <i class="fas ${btn.icon}"></i> ${btn.label}
          </button>
        `).join('')}
      </div>
      <div class="elaborate-info hidden">
        ${Object.entries(promptData.elaborateInfo).map(([section, items]) => `
          <div class="elaborate-section">
            <h3>${section}</h3>
            <ul>${items.map(item => `<li>${item}</li>`).join('')}</ul>
          </div>
        `).join('')}
      </div>
    </div>
  `;
}

processCouponQuery(query) {
    const normalizedQuery = query.toLowerCase();
    const words = normalizedQuery.split(' ');
    
    const hasCouponKeyword = searchConfig.couponDatabase.keywords.some(keyword => 
      words.includes(keyword.toLowerCase())
    );
    
    if (!hasCouponKeyword) return null;
    
    const brand = searchConfig.couponDatabase.brands.find(brand => 
      words.includes(brand.toLowerCase())
    );
    
    if (brand) {
      return this.generateCouponResponse([brand]);
    } else {
      return this.generateCouponResponse(searchConfig.couponDatabase.brands);
    }
  }

  generateCouponResponse(brands) {
    let couponsHTML = '';
    
    brands.forEach(brand => {
      const coupons = searchConfig.couponDatabase.items[brand];
      if (coupons && coupons.length > 0) {
        couponsHTML += coupons.map(coupon => `
          <div class="coupon-item" onclick="toggleCouponInfo(this)">
            <div class="coupon-header">
              <div class="brand-info">
                <i class="fas ${coupon.icon}"></i>
                <span>${coupon.brand}</span>
              </div>
              <div class="discount-tag">${coupon.discount}</div>
            </div>
            
            <div class="coupon-content">
              <p class="description">${coupon.description}</p>
              <div class="code-container">
                <code class="coupon-code">${coupon.code}</code>
                <button class="copy-button" onclick="event.stopPropagation(); copyCouponCode('${coupon.code}')">
                  <i class="fas fa-copy"></i>
                </button>
              </div>
              <div class="validity">Valid till: ${coupon.validity}</div>
            </div>
            
            <div class="coupon-info hidden">
              ${Object.entries(coupon.eligibility).map(([section, items]) => `
                <div class="info-section">
                  <h4>${section}</h4>
                  ${Array.isArray(items) 
                    ? `<ul>${items.map(item => `<li>${item}</li>`).join('')}</ul>`
                    : `<p>${items}</p>`
                  }
                </div>
              `).join('')}
            </div>
          </div>
        `).join('');
      }
    });

    return `
      <div class="coupons-container">
        <h2>Available Coupons</h2>
        ${couponsHTML}
      </div>
    `;
  }

  searchDatabase(query) {
    const normalizedQuery = query.toLowerCase();
    const words = normalizedQuery.split(/\s+/);
    const results = [];

    for (const [question, data] of Object.entries(searchConfig.qaDatabase)) {
      if (normalizedQuery === question.toLowerCase()) {
        results.push({ similarity: 1, data });
        continue;
      }

      const keywordMatch = data.keywords?.some(keyword => 
        words.includes(keyword.toLowerCase())
      );
      if (keywordMatch) {
        results.push({ similarity: 0.8, data });
        continue;
      }

      const similarity = this.calculateSimilarity(normalizedQuery, question.toLowerCase());
      if (similarity > this.similarityThreshold) {
        results.push({ similarity, data });
      }
    }
    return results;
  }

  calculateSimilarity(str1, str2) {
    const words1 = str1.split(/\s+/);
    const words2 = str2.split(/\s+/);
    const set1 = new Set(words1);
    const set2 = new Set(words2);
    const intersection = new Set([...set1].filter(x => set2.has(x)));
    const union = new Set([...set1, ...set2]);
    const jaccardSimilarity = intersection.size / union.size;
    
    let orderSimilarity = 0;
    words1.forEach((word, index) => {
      const pos2 = words2.indexOf(word);
      if (pos2 !== -1) {
        orderSimilarity += 1 - Math.abs(index - pos2) / Math.max(words1.length, words2.length);
      }
    });
    
    return (jaccardSimilarity * 0.7) + (orderSimilarity / words1.length * 0.3);
  }

  getRandomFallbackResponse() {
    const responses = searchConfig.fallbackResponses;
    return responses[Math.floor(Math.random() * responses.length)];
  }

  displayMessage(content, type) {
    const messageDiv = document.createElement('div');
    messageDiv.className = `message ${type}-message`;
    
    if (type === 'bot') {
      messageDiv.innerHTML = `
        <div class="message-avatar"><i class="fas fa-comments"></i></div>
        <div class="message-content">${content}</div>`;
    } else {
      messageDiv.innerHTML = `
        <div class="message-content">${content}</div>`;
    }
    
    this.chatMessages.appendChild(messageDiv);
  }

  async simulateProcessing() {
    const typingIndicator = document.createElement('div');
    typingIndicator.className = 'message bot-message typing-indicator';
    typingIndicator.innerHTML = '<div class="dots"><span>.</span><span>.</span><span>.</span></div>';
    this.chatMessages.appendChild(typingIndicator);
    this.scrollToBottom();
    await new Promise(resolve => setTimeout(resolve, 1000));
    typingIndicator.remove();
  }

  scrollToBottom() {
    this.chatMessages.scrollTop = this.chatMessages.scrollHeight;
  }
}

// Menu System Implementation
function setupMenu() {
  const menuButton = document.getElementById('menuButton');
  const menuOverlay = document.getElementById('menuOverlay');
  const menuItems = document.querySelectorAll('.menu-item');
  const chatMessages = document.getElementById('chatMessages');
  
  const closeButton = document.createElement('button');
  closeButton.innerHTML = '<i class="fas fa-long-arrow-alt-left"></i>';
  closeButton.className = 'menu-close-button';
  menuOverlay.appendChild(closeButton);

  function toggleMenu(show) {
      menuOverlay.style.display = show ? 'block' : 'none';
      menuOverlay.classList.toggle('fade-in', show);
      document.body.style.overflow = show ? 'hidden' : '';
  }

  menuButton.addEventListener('click', () => toggleMenu(true));
  closeButton.addEventListener('click', () => toggleMenu(false));
  menuOverlay.addEventListener('click', (e) => {
      if (e.target === menuOverlay) toggleMenu(false);
  });

  menuItems.forEach(item => {
      item.addEventListener('click', () => {
          const selectedItem = item.textContent.trim();
          const message = document.createElement('div');
          message.className = 'message bot-message';
          message.innerHTML = `
              <div class="message-avatar"><i class="fas fa-comments"></i></div>
              <div class="message-content">You selected: ${selectedItem}. How can I assist you further?</div>
          `;
          chatMessages.appendChild(message);
          chatMessages.scrollTop = chatMessages.scrollHeight;
          toggleMenu(false);
      });
  });

  document.addEventListener('keydown', (e) => {
      if (e.key === 'Escape') toggleMenu(false);
  });
}

// Utility function to toggle detailed information
function toggleDetailedInfo(element) {
  const infoPanel = element.closest('.list-item').querySelector('.detailed-info');
  infoPanel.classList.toggle('hidden');
}

function toggleElaborateInfo(promptResponse) {
    const infoPanel = promptResponse.querySelector('.elaborate-info');
    infoPanel.classList.toggle('hidden');
}


// Utility functions
function toggleCouponInfo(element) {
  const infoPanel = element.querySelector('.coupon-info');
  infoPanel.classList.toggle('hidden');
}

function copyCouponCode(code) {
  navigator.clipboard.writeText(code).then(() => {
    showToast('Coupon code copied!');
  }).catch(err => {
    showToast('Failed to copy code');
  });
}

function showToast(message) {
  const toast = document.createElement('div');
  toast.className = 'toast';
  toast.textContent = message;
  document.body.appendChild(toast);
  
  setTimeout(() => {
    toast.classList.add('show');
    setTimeout(() => {
      toast.classList.remove('show');
      setTimeout(() => toast.remove(), 300);
    }, 2000);
  }, 100);
}

document.addEventListener('DOMContentLoaded', function() {
  const chatSystem = new ChatSystem();
  chatSystem.initialize();
  setupMenu();

  if (typeof flatpickr !== 'undefined') {
      flatpickr("#dateInput", {
          minDate: "today",
          maxDate: new Date().fp_incr(30),
          dateFormat: "Y-m-d"
      });

      flatpickr("#timeInput", {
          enableTime: true,
          noCalendar: true,
          dateFormat: "H:i",
          minTime: "09:00",
          maxTime: "18:00",
          minuteIncrement: 30
      });
  }
});

const style = document.createElement('style');
style.textContent = `
  .typing-indicator {
      padding: 20px;
  }

  .typing-indicator .dots {
      display: inline-flex;
      gap: 4px;
  }

  .typing-indicator .dots span {
      width: 8px;
      height: 8px;
      background: #666;
      border-radius: 50%;
      animation: bounce 1.4s infinite ease-in-out;
  }

  .typing-indicator .dots span:nth-child(1) { animation-delay: -0.32s; }
  .typing-indicator .dots span:nth-child(2) { animation-delay: -0.16s; }

  @keyframes bounce {
      0%, 80%, 100% { transform: scale(0); }
      40% { transform: scale(1); }
  }

    .message {
    display: flex; 
    gap: 10px; 
    max-width: 100%; 
    margin-bottom: 16px; 
    animation: messageSlide 0.3s ease-out; 
    }

    .bot-message { 
  align-self: flex-start; 
}
   
   .user-message {
        background: #lalala;
        color: white;
        margin-left: auto;
    }

    .message-avatar {
        width: 30px;
        height: 30px;
        background: #lalala;
        color: #FFD700;
        border-radius: 50%;
        display: flex;
        align-items: center;
        justify-content: center;
    }

    .welcome-message ul {
        margin: 10px 0;
        padding-left:20px;
    }

    .menu-close-button {
        position: absolute;
        top: 15px;
        right: 15px;
        background: #1a1a1f;
        border: none;
        color: #FFD700;
        font-size: 24px;
        cursor: pointer;
        padding: 5px;
        z-index: 1001;
    }

    .menu-close-button:hover {
        color: #FFD700;
    }

.prompt-response {
  background: #lalala;
  color: white;
  margin-left: auto;
  position: relative;  /* Add relative positioning for absolute child */
}

    .click-buttons {
        display: flex;
        align-items: center;
        gap: 8px;
        margin-top: 10px;
        height: 40px;
        pointer-events: none; /* Prevent action buttons from triggering detailed info */
    }

    .click-button {
        pointer-events: auto; /* Re-enable clicks for action buttons */
        padding: 8px 16px;
        background: linear-gradient(to bottom, #2563eb, #1d4ed8);
        color: white;
        border: none;
        border-radius: 6px;
        cursor: pointer;
        display: flex;
        align-items: center;
        gap: 8px;
        font-weight: 500;
        transition: all 0.2s ease;
        box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
        height: 40px;
        line-height: 40px;
    }

    .click-button:hover {
        background: linear-gradient(to bottom, #1d4ed8, #1e40af);
        transform: translateY(-1px);
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.15);
    }

    .elaborate-info {
        margin-top: 15px;
        padding: 15px;
        background: #lalala;
        border-radius: 4px;
        clear: both;
        animation: fadeIn 0.3s ease-out;
    }

    .hidden {
        display: none;
    }

    .elaborate-section {
        margin-bottom: 15px;
    }

    .elaborate-section h3 {
        margin-bottom: 8px;
        color: #fff;
    }

    .elaborate-section ul {
        margin: 0;
        padding-left: 20px;
    }

.list-container {
  background: #lalala;
  color: white;
  margin-left: auto;
  position: relative;  /* Add relative positioning for absolute child */
}

.list-item {
  background: var(--item-bg, #lalala);
  border-radius: 8px;
  padding: clamp(10px, 3vw, 15px);
  margin-bottom: 12px;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
  cursor: pointer;
  user-select: none;
  width: 100%;
}

@media (hover: hover) {
  .list-item:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  }
}

.item-header {
  display: flex;
  flex-direction: column;
  gap: 8px;
  margin-bottom: 10px;
}

@media (min-width: 480px) {
  .item-header {
    flex-direction: row;
    justify-content: space-between;
    align-items: center;
  }
}

.rating {
  color: #ffd700;
  font-weight: bold;
}

.item-content {
  margin-bottom: 12px;
  word-break: break-word;
}

.item-specific {
  font-size: 0.9em;
  color: #fff;
  margin: 4px 0;
}

.item-actions {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  width: 100%;
}

.touch-button {
  padding: 8px 16px;
  background: linear-gradient(to bottom, #2563eb, #1d4ed8);
  color: white;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  gap: 8px;
  font-weight: 500;
  transition: transform 0.2s ease;
  flex: 1 1 auto;
  justify-content: center;
  min-width: 120px;
  max-width: 200px;
}

@media (max-width: 479px) {
  .touch-button {
    width: 100%;
    max-width: none;
  }
}

.detailed-info {
        margin-top: 15px;
        padding: 15px;
        background: #lalala;
        border-radius: 4px;
        clear: both;
        animation: fadeIn 0.3s ease-out;
    }

.info-section {
  margin-bottom: 12px;
}

.info-section h3 {
  color: #fff;
  margin-bottom: 8px;
  font-size: 12px;
  padding-left: 0px;
}

.info-section h4 {
  color: #fff;
  margin-bottom: 8px;
  font-size: clamp(1rem, 2.5vw, 1.25rem);
   margin-left: -14px;
}

.info-section ul {
  margin: 0;
  margin-left: 0px;
  color: #fff;
}

.hidden {
  display: none;
}

  .coupons-container {
    display: flex;
    flex-direction: column;
    gap: 16px;
    width: 100%;
    max-width: 600px;
  }

  .coupon-item {
    background: #1a1a1f;
    border-radius: 12px;
    padding: 16px;
    cursor: pointer;
    transition: transform 0.2s ease, box-shadow 0.2s ease;
    border: 1px solid rgba(255, 255, 255, 0.1);
  }

  .coupon-item:hover {
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.2);
  }

  .coupon-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 12px;
  }

  .brand-info {
    display: flex;
    align-items: center;
    gap: 8px;
    font-weight: 500;
  }

  .brand-info i {
    font-size: 20px;
    color: #FFD700;
  }

  .discount-tag {
    background: linear-gradient(135deg, #2563eb, #1d4ed8);
    color: white;
    padding: 4px 8px;
    margin-left: 18px;
    border-radius: 4px;
    font-weight: 600;
  }

  .coupon-content {
    margin-bottom: 12px;
  }

  .description {
    margin-bottom: 8px;
    color: #fff;
  }

  .code-container {
    display: flex;
    align-items: center;
    gap: 8px;
    margin: 12px 0;
    background: rgba(255, 255, 255, 0.05);
    padding: 8px;
    border-radius: 6px;
  }

  .coupon-code {
    font-family: monospace;
    font-size: 16px;
    letter-spacing: 1px;
    color: #FFD700;
    background: transparent;
  }

  .copy-button {
    background: transparent;
    border: none;
    color: #FFD700;
    cursor: pointer;
    padding: 4px 8px;
    transition: transform 0.2s ease;
  }

  .copy-button:hover {
    transform: scale(1.1);
  }

  .validity {
    font-size: 0.9em;
    color: #888;
  }

  .toast {
    position: fixed;
    bottom: 20px;
    left: 50%;
    transform: translateX(-50%) translateY(100px);
    background: rgba(0, 0, 0, 0.8);
    color: white;
    padding: 12px 24px;
    border-radius: 8px;
    transition: transform 0.3s ease;
    z-index: 1000;
  }

  .toast.show {
    transform: translateX(-50%) translateY(0);
  }

  .coupon-info {
    margin-top: 16px;
    padding-top: 16px;
    border-top: 1px solid rgba(255, 255, 255, 0.1);
  }

  .coupon-info .info-section {
    margin-bottom: 12px;
  }

  .coupon-info h4 {
    font-size: 14.9px;
    margin-left: 0px;
    color: #FFD700;
    margin-bottom: 8px;
  }

  .coupon-info ul {
    font-size: 14px;
    margin-left: 0px;
    list-style: none;
    padding-left: 0;
  }

  .coupon-info li {
    color: #fff;
    margin-bottom: 4px;
    position: relative;
    padding-left: 20px;
  }

  .coupon-info li:before {
    content: '•';
    position: absolute;
    left: 0;
    color: #FFD700;
  }

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }

  @keyframes messageSlide {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
  }
`;

document.head.appendChild(style);

                const townsData = [
  {
    name: "Mumbai",
    image: "https://i.pinimg.com/originals/2c/72/40/2c72408b797d4841b6fe6c395183ba35.png",
    quote: "The town of dreams where ambitions take flight and opportunities never sleep"
  },
  {
    name: "Delhi",
    image: "https://www.mistay.in/travel-blog/content/images/2020/07/travel-4813658_1920.jpg",
    quote: "Where ancient heritage meets modern aspirations in perfect harmony"
  },
  {
    name: "Jaipur",
    image: "https://www.tripsavvy.com/thmb/Afl1v6bgmGid9kPfseymDiAYWa0=/3595x2397/filters:no_upscale():max_bytes(150000):strip_icc()/GettyImages-518387310-04a30994bfb1461bb8000f1864ca1fc5.jpg",
    quote: "Pink Town, where royal heritage colors modern dreams"
  }
];

function showTownsOverlay() {
  let overlay = document.getElementById('townsOverlay');
  if (!overlay) {
    overlay = document.createElement('div');
    overlay.id = 'townsOverlay';
    overlay.className = 'towns-overlay';
    document.body.appendChild(overlay);
  }
  overlay.innerHTML = `
    <div class="towns-content">
      <div class="towns-header">
        <h2>Cities We Serve</h2>
        <button class="close-towns" onclick="hideTownsOverlay()">
          <i class="fas fa-long-arrow-alt-left"></i>
        </button>
      </div>
      <div class="towns-grid">
        ${townsData.map(town => `
          <div class="town-card" onclick="selectTown('${town.name}')">
            <div class="town-image-container">
              <img src="${town.image}" alt="${town.name}" class="town-image">
              <div class="town-overlay"></div>
            </div>
            <div class="town-info">
              <h3 class="town-name">${town.name}</h3>
              <p class="town-quote">${town.quote}</p>
            </div>
          </div>
        `).join('')}
      </div>
    </div>
  `;
  setTimeout(() => overlay.classList.add('active'), 10);

  const style = document.createElement('style');
  style.textContent = `
.towns-overlay {
  position: fixed;
  top: 60px;
  left: 0;
  right: 0;
  bottom: 60px;
  background:  #000000;
  z-index: 1000;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
  overflow-y: auto;
}

.towns-overlay.active {
  opacity: 1;
  visibility: visible;
}

.towns-content {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
}

.towns-header {
  padding: 8px 16px;
  background: rgba(26, 26, 31, 0.95);
  position: fixed;
  width: 100%;
  top: 0;
  left: 0;
  z-index: 30;
  border-bottom: 2px solid var(--primary-color);
  backdrop-filter: blur(10px);
  height: 65px;
  /* Flexbox for horizontal layout */
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 5px;
}

.towns-header h2 {
  color: var(--primary-color);
  margin: 0;
  font-size: 1.5em;
  flex-grow: 0;
}

.close-towns {
  background: none;
  border: none;
  color: var(--primary-color);
  font-size: 1.5em;
  cursor: pointer;
  padding: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.towns-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
  animation: fadeInUp 0.5s ease-out;
  margin-top: 10px; /* Ensure content starts below the header */
}

.town-card {
  border-radius: 12px;
  overflow: hidden;
  background: rgba(26, 26, 31, 0.98);
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
}

.town-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

.town-image-container {
  position: relative;
  width: 100%;
  height: 200px;
  overflow: hidden;
}

.town-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.town-card:hover .town-image {
  transform: scale(1.1);
}

.town-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.town-info {
  padding: 20px;
  position: relative;
  z-index: 1;
}

.town-name {
  color: var(--text-light);
  margin: 0 0 10px 0;
  font-size: 1.4em;
}

.town-quote {
  color: #cccccc;
  font-size: 0.9em;
  line-height: 1.4;
  margin: 0;
}

    .list-container {
      padding: 15px;
      background: #f8f9fa;
      border-radius: 8px;
    }

    .list-item {
      background: white;
      border-radius: 8px;
      padding: 15px;
      margin-bottom: 15px;
      box-shadow: 0 2px 4px rgba(0,0,0,0.1);
      transition: all 0.3s ease;
    }

    .list-item:hover {
      transform: translateY(-2px);
      box-shadow: 0 4px 8px rgba(0,0,0,0.15);
    }

    .item-header {
      display: flex;
      justify-content: space-between;
      align-items: center;
      margin-bottom: 10px;
    }

    .rating {
      color: #ffd700;
      font-weight: bold;
    }

    .item-content {
      margin-bottom: 15px;
    }

    .item-specific {
      font-size: 0.9em;
      color: #666;
      margin: 5px 0;
    }

    .item-actions {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
    }

    .action-button {
      padding: 8px 16px;
      background: linear-gradient(to bottom, #2563eb, #1d4ed8);
      color: white;
      border: none;
      border-radius: 6px;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 8px;
      font-weight: 500;
      transition: all 0.2s ease;
    }

    .action-button:hover {
      background: linear-gradient(to bottom, #1d4ed8, #1e40af);
      transform: translateY(-1px);
    }

    .info-button {
      background: #6c757d;
      color: white;
      border: none;
      border-radius: 6px;
      padding: 8px 16px;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 8px;
      transition: all 0.2s ease;
    }

    .info-button:hover {
      background: #5a6268;
    }

    .detailed-info {
      margin-top: 15px;
      padding: 15px;
      background: #f8f9fa;
      border-radius: 4px;
      animation: fadeIn 0.3s ease-out;
    }

    .hidden {
      display: none;
    }

    .info-section {
      margin-bottom: 15px;
    }

    .info-section h4 {
      margin-bottom: 8px;
      color: #333;
    }

    .info-section ul {
      margin: 0;
      padding-left: 20px;
    }

    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(10px); }
      to { opacity: 1; transform: translateY(0); }
    }
  
@keyframes fadeInUp {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}

@media (max-width: 768px) {
  .towns-grid {
    grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  }
  
  .town-image-container {
    height: 160px;
  }
}
    `;
  document.head.appendChild(style);
}

function hideTownsOverlay() {
  const overlay = document.getElementById('townsOverlay');
  if (overlay) {
    overlay.classList.remove('active');
    setTimeout(() => overlay.remove(), 300);
  }
}

function selectTown(townName) {
  console.log(`Selected town: ${townName}`);
  showAlert(`Selected location: ${townName}`, 'success');
  hideTownsOverlay();
}
              
document.addEventListener('DOMContentLoaded', function() {
    // Select the location link in the menu section
    const menuLocationLink = document.querySelector('.menu-section .location-link');
    
    if (menuLocationLink) {
        menuLocationLink.addEventListener('click', function(e) {
            e.preventDefault(); // Prevent default link behavior
            showTownsOverlay(); // Call the existing function to show towns overlay
        });
    }
});

const locatorsData = [
  // Delhi
  {
    category: "Grocery",
    metropolis: "Delhi",
    details: {
      name: "Dmart",
      image: "https://www.projectsmonitor.com/wp-content/uploads/2021/09/@DMartOfficiall.jpg",
      description: "Your favorite destination for groceries and household essentials at unbeatable prices.",
      address: "Karol Bagh, Delhi",
      timings: "Mon-Sun: 9 AM - 10 PM",
      payment: "Cash, Credit/Debit Cards, UPI",
      mapLink: "https://maps.example.com/dmart",
      menuLink: "https://www.dmart.in/",
      images: [
        "https://www.projectsmonitor.com/wp-content/uploads/2021/09/@DMartOfficiall.jpg",
        "https://www.goodreturns.in/img/1200x60x675/2020/04/dmart-1525851463-1586576977.jpg"
      ],
      social: {
        facebook: "https://facebook.com/dmart",
        twitter: "https://twitter.com/dmart",
        instagram: "https://instagram.com/dmart"
      },
      menu: [
        { name: "Rice", price: "$10/5kg", image: "https://example.com/rice.jpg" },
        { name: "Wheat Flour", price: "$8/5kg", image: "https://example.com/wheat.jpg" }
      ],
      promos: [
        { code: "DMART10", description: "Get 10% off on your first order" }
      ],
      support: {
        email: "support@dmart.com",
        phone: "+91-1234567890"
      },
      outlets: [
        {
          name: "Dmart Karol Bagh",
          address: "Karol Bagh, Delhi",
          timings: "Mon-Sun: 9 AM - 10 PM",
          mapLink: "https://maps.example.com/dmart-karol-bagh"
        },
        {
          name: "Dmart Connaught Place",
          address: "Connaught Place, Delhi",
          timings: "Mon-Sun: 9 AM - 10 PM",
          mapLink: "https://maps.example.com/dmart-connaught-place"
        }
      ]
    }
  },
  {
    category: "Food",
    metropolis: "Delhi",
    details: {
      name: "Burger King",
      image: "https://example.com/burgerking.jpg",
      description: "Home of the Whopper. Flame-grilled burgers and fries.",
      address: "Connaught Place, Delhi",
      timings: "Mon-Sun: 10 AM - 11 PM",
      payment: "Cash, Credit/Debit Cards, UPI",
      mapLink: "https://maps.example.com/burgerking",
      menuLink: "https://www.burgerking.in/",
      images: [
        "https://example.com/burgerking1.jpg",
        "https://example.com/burgerking2.jpg"
      ],
      social: {
        facebook: "https://facebook.com/burgerking",
        twitter: "https://twitter.com/burgerking",
        instagram: "https://instagram.com/burgerking"
      },
      menu: [
        { name: "Whopper", price: "$5.99", image: "https://example.com/whopper.jpg" },
        { name: "Chicken Fries", price: "$3.99", image: "https://example.com/chicken-fries.jpg" }
      ],
      promos: [
        { code: "BK15", description: "Get 15% off on your first order" }
      ],
      support: {
        email: "support@burgerking.com",
        phone: "+91-9876543210"
      },
      outlets: [
        {
          name: "Burger King Connaught Place",
          address: "Connaught Place, Delhi",
          timings: "Mon-Sun: 10 AM - 11 PM",
          mapLink: "https://maps.example.com/burgerking-cp"
        },
        {
          name: "Burger King Saket",
          address: "Saket, Delhi",
          timings: "Mon-Sun: 10 AM - 11 PM",
          mapLink: "https://maps.example.com/burgerking-saket"
        }
      ]
    }
  },
  {
    category: "Electronics",
    metropolis: "Delhi",
    details: {
      name: "Reliance Digital",
      image: "https://example.com/reliancedigital.jpg",
      description: "Your one-stop shop for electronics and appliances.",
      address: "Nehru Place, Delhi",
      timings: "Mon-Sun: 10 AM - 9 PM",
      payment: "Cash, Credit/Debit Cards, UPI",
      mapLink: "https://maps.example.com/reliancedigital",
      menuLink: "https://www.reliancedigital.in/",
      images: [
        "https://example.com/reliancedigital1.jpg",
        "https://example.com/reliancedigital2.jpg"
      ],
      social: {
        facebook: "https://facebook.com/reliancedigital",
        twitter: "https://twitter.com/reliancedigital",
        instagram: "https://instagram.com/reliancedigital"
      },
      menu: [
        { name: "Smart TV", price: "$500", image: "https://example.com/smarttv.jpg" },
        { name: "Laptop", price: "$800", image: "https://example.com/laptop.jpg" }
      ],
      promos: [
        { code: "RD10", description: "Get 10% off on electronics" }
      ],
      support: {
        email: "support@reliancedigital.com",
        phone: "+91-9876543210"
      },
      outlets: [
        {
          name: "Reliance Digital Nehru Place",
          address: "Nehru Place, Delhi",
          timings: "Mon-Sun: 10 AM - 9 PM",
          mapLink: "https://maps.example.com/reliancedigital-nehru-place"
        },
        {
          name: "Reliance Digital Rajouri Garden",
          address: "Rajouri Garden, Delhi",
          timings: "Mon-Sun: 10 AM - 9 PM",
          mapLink: "https://maps.example.com/reliancedigital-rajouri-garden"
        }
      ]
    }
  },

  // Mumbai
  {
    category: "Grocery",
    metropolis: "Mumbai",
    details: {
      name: "Big Bazaar",
      image: "https://example.com/bigbazaar.jpg",
      description: "India's largest hypermarket chain for groceries and more.",
      address: "Andheri, Mumbai",
      timings: "Mon-Sun: 9 AM - 10 PM",
      payment: "Cash, Credit/Debit Cards, UPI",
      mapLink: "https://maps.example.com/bigbazaar",
      menuLink: "https://www.bigbazaar.com/",
      images: [
        "https://example.com/bigbazaar1.jpg",
        "https://example.com/bigbazaar2.jpg"
      ],
      social: {
        facebook: "https://facebook.com/bigbazaar",
        twitter: "https://twitter.com/bigbazaar",
        instagram: "https://instagram.com/bigbazaar"
      },
      menu: [
        { name: "Rice", price: "$10/5kg", image: "https://example.com/rice.jpg" },
        { name: "Cooking Oil", price: "$15/5L", image: "https://example.com/cooking-oil.jpg" }
      ],
      promos: [
        { code: "BB20", description: "Get 20% off on groceries" }
      ],
      support: {
        email: "support@bigbazaar.com",
        phone: "+91-9876543210"
      },
      outlets: [
        {
          name: "Big Bazaar Andheri",
          address: "Andheri, Mumbai",
          timings: "Mon-Sun: 9 AM - 10 PM",
          mapLink: "https://maps.example.com/bigbazaar-andheri"
        },
        {
          name: "Big Bazaar Borivali",
          address: "Borivali, Mumbai",
          timings: "Mon-Sun: 9 AM - 10 PM",
          mapLink: "https://maps.example.com/bigbazaar-borivali"
        }
      ]
    }
  },
  {
    category: "Food",
    metropolis: "Mumbai",
    details: {
      name: "McDonald's",
      image: "https://wallpapercave.com/wp/wp11260474.png",
      description: "The home of world-famous burgers and fries.",
      address: "Bandra, Mumbai",
      timings: "Mon-Sun: 10 AM - 11 PM",
      payment: "Cash, Credit/Debit Cards, UPI",
      mapLink: "https://maps.example.com/mcdonalds",
      menuLink: "https://mcdelivery.co.in/menu",
      images: [
        "https://example.com/mcd1.jpg",
        "https://example.com/mcd2.jpg"
      ],
      social: {
        facebook: "https://facebook.com/mcdonalds",
        twitter: "https://twitter.com/mcdonalds",
        instagram: "https://instagram.com/mcdonalds"
      },
      menu: [
        { name: "Big Mac", price: "$5.99", image: "https://example.com/bigmac.jpg" },
        { name: "French Fries", price: "$2.99", image: "https://example.com/fries.jpg" }
      ],
      promos: [
        { code: "MCD20", description: "Get 20% off on orders above $20" }
      ],
      support: {
        email: "support@mcdonalds.com",
        phone: "+91-9876543210"
      },
      outlets: [
        {
          name: "McDonald's Bandra",
          address: "Bandra, Mumbai",
          timings: "Mon-Sun: 10 AM - 11 PM",
          mapLink: "https://maps.example.com/mcdonalds-bandra"
        },
        {
          name: "McDonald's Andheri",
          address: "Andheri, Mumbai",
          timings: "Mon-Sun: 10 AM - 11 PM",
          mapLink: "https://maps.example.com/mcdonalds-andheri"
        }
      ]
    }
  },
  {
    category: "Electronics",
    metropolis: "Mumbai",
    details: {
      name: "Vijay Sales",
      image: "https://example.com/vijaysales.jpg",
      description: "Your trusted destination for electronics and appliances.",
      address: "Dadar, Mumbai",
      timings: "Mon-Sun: 10 AM - 9 PM",
      payment: "Cash, Credit/Debit Cards, UPI",
      mapLink: "https://maps.example.com/vijaysales",
      menuLink: "https://www.vijaysales.com/",
      images: [
        "https://example.com/vijaysales1.jpg",
        "https://example.com/vijaysales2.jpg"
      ],
      social: {
        facebook: "https://facebook.com/vijaysales",
        twitter: "https://twitter.com/vijaysales",
        instagram: "https://instagram.com/vijaysales"
      },
      menu: [
        { name: "Smart TV", price: "$500", image: "https://example.com/smarttv.jpg" },
        { name: "Refrigerator", price: "$700", image: "https://example.com/refrigerator.jpg" }
      ],
      promos: [
        { code: "VS15", description: "Get 15% off on electronics" }
      ],
      support: {
        email: "support@vijaysales.com",
        phone: "+91-9876543210"
      },
      outlets: [
        {
          name: "Vijay Sales Dadar",
          address: "Dadar, Mumbai",
          timings: "Mon-Sun: 10 AM - 9 PM",
          mapLink: "https://maps.example.com/vijaysales-dadar"
        },
        {
          name: "Vijay Sales Thane",
          address: "Thane, Mumbai",
          timings: "Mon-Sun: 10 AM - 9 PM",
          mapLink: "https://maps.example.com/vijaysales-thane"
        }
      ]
    }
  },

  // Bangalore
  {
    category: "Grocery",
    metropolis: "Bangalore",
    details: {
      name: "More Megastore",
      image: "https://example.com/moremegastore.jpg",
      description: "A wide range of groceries and household items.",
      address: "Koramangala, Bangalore",
      timings: "Mon-Sun: 9 AM - 10 PM",
      payment: "Cash, Credit/Debit Cards, UPI",
      mapLink: "https://maps.example.com/moremegastore",
      menuLink: "https://www.moremegastore.com/",
      images: [
        "https://example.com/moremegastore1.jpg",
        "https://example.com/moremegastore2.jpg"
      ],
      social: {
        facebook: "https://facebook.com/moremegastore",
        twitter: "https://twitter.com/moremegastore",
        instagram: "https://instagram.com/moremegastore"
      },
      menu: [
        { name: "Rice", price: "$10/5kg", image: "https://example.com/rice.jpg" },
        { name: "Cooking Oil", price: "$15/5L", image: "https://example.com/cooking-oil.jpg" }
      ],
      promos: [
        { code: "MORE10", description: "Get 10% off on groceries" }
      ],
      support: {
        email: "support@moremegastore.com",
        phone: "+91-9876543210"
      },
      outlets: [
        {
          name: "More Megastore Koramangala",
          address: "Koramangala, Bangalore",
          timings: "Mon-Sun: 9 AM - 10 PM",
          mapLink: "https://maps.example.com/moremegastore-koramangala"
        },
        {
          name: "More Megastore Whitefield",
          address: "Whitefield, Bangalore",
          timings: "Mon-Sun: 9 AM - 10 PM",
          mapLink: "https://maps.example.com/moremegastore-whitefield"
        }
      ]
    }
  },
  {
    category: "Food",
    metropolis: "Bangalore",
    details: {
      name: "Domino's Pizza",
      image: "https://example.com/dominos.jpg",
      description: "Hot, fresh pizza delivered to your doorstep.",
      address: "Indiranagar, Bangalore",
      timings: "Mon-Sun: 11 AM - 11 PM",
      payment: "Cash, Credit/Debit Cards, UPI",
      mapLink: "https://maps.example.com/dominos",
      menuLink: "https://www.dominos.co.in/",
      images: [
        "https://example.com/dominos1.jpg",
        "https://example.com/dominos2.jpg"
      ],
      social: {
        facebook: "https://facebook.com/dominos",
        twitter: "https://twitter.com/dominos",
        instagram: "https://instagram.com/dominos"
      },
      menu: [
        { name: "Margherita Pizza", price: "$8", image: "https://example.com/margherita.jpg" },
        { name: "Pepperoni Pizza", price: "$10", image: "https://example.com/pepperoni.jpg" }
      ],
      promos: [
        { code: "DOMINOS20", description: "Get 20% off on your first order" }
      ],
      support: {
        email: "support@dominos.com",
        phone: "+91-9876543210"
      },
      outlets: [
        {
          name: "Domino's Indiranagar",
          address: "Indiranagar, Bangalore",
          timings: "Mon-Sun: 11 AM - 11 PM",
          mapLink: "https://maps.example.com/dominos-indiranagar"
        },
        {
          name: "Domino's Koramangala",
          address: "Koramangala, Bangalore",
          timings: "Mon-Sun: 11 AM - 11 PM",
          mapLink: "https://maps.example.com/dominos-koramangala"
        }
      ]
    }
  },
  {
    category: "Electronics",
    metropolis: "Bangalore",
    details: {
      name: "Croma",
      image: "https://example.com/croma.jpg",
      description: "Your one-stop shop for all electronics and appliances.",
      address: "MG Road, Bangalore",
      timings: "Mon-Sun: 10 AM - 9 PM",
      payment: "Cash, Credit/Debit Cards, UPI",
      mapLink: "https://maps.example.com/croma",
      menuLink: "https://www.croma.com/",
      images: [
        "https://example.com/croma1.jpg",
        "https://example.com/croma2.jpg"
      ],
      social: {
        facebook: "https://facebook.com/croma",
        twitter: "https://twitter.com/croma",
        instagram: "https://instagram.com/croma"
      },
      menu: [
        { name: "Smart TV", price: "$500", image: "https://example.com/smarttv.jpg" },
        { name: "Laptop", price: "$800", image: "https://example.com/laptop.jpg" }
      ],
      promos: [
        { code: "CROMA15", description: "Get 15% off on electronics" }
      ],
      support: {
        email: "support@croma.com",
        phone: "+91-9876543210"
      },
      outlets: [
        {
          name: "Croma MG Road",
          address: "MG Road, Bangalore",
          timings: "Mon-Sun: 10 AM - 9 PM",
          mapLink: "https://maps.example.com/croma-mg-road"
        },
        {
          name: "Croma Whitefield",
          address: "Whitefield, Bangalore",
          timings: "Mon-Sun: 10 AM - 9 PM",
          mapLink: "https://maps.example.com/croma-whitefield"
        }
      ]
    }
  }
];

// Debounce function to limit the rate of search execution
function debounce(func, wait) {
  let timeout;
  return function executedFunction(...args) {
    const later = () => {
      clearTimeout(timeout);
      func(...args);
    };
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
}

// Function to normalize text for better matching
function normalizeText(text) {
  return text.toLowerCase().trim();
}

// Function to check if a string contains words in any order
function containsWordsInAnyOrder(text, searchWords) {
  text = normalizeText(text);
  return searchWords.every(word => text.includes(word));
}

// Main search function
function searchLocators(searchQuery) {
  const locatorsGrid = document.getElementById('locatorsGrid');
  if (!searchQuery.trim()) {
    locatorsGrid.innerHTML = renderLocatorCards(locatorsData);
    return;
  }

  // Normalize search query and split into words
  const searchWords = normalizeText(searchQuery).split(/\s+/);

  // Search through locations with intent understanding
  const results = locatorsData.filter(locator => {
    const searchableText = `
      ${locator.category} 
      ${locator.metropolis} 
      ${locator.details.name} 
      ${locator.details.description} 
      ${locator.details.address}
      ${locator.details.payment || ''}
      ${(locator.details.menu || []).map(item => item.name).join(' ')}
    `.toLowerCase();

    // Check for exact matches first
    if (searchableText.includes(searchQuery.toLowerCase())) {
      return true;
    }

    // Check for category + city combinations
    if (searchWords.includes(normalizeText(locator.category)) && 
        searchWords.includes(normalizeText(locator.metropolis))) {
      return true;
    }

    // Check for words in any order
    return containsWordsInAnyOrder(searchableText, searchWords);
  });

  // Sort results by relevance
  const sortedResults = results.sort((a, b) => {
    const aText = `${a.category} ${a.metropolis} ${a.details.name}`.toLowerCase();
    const bText = `${b.category} ${b.metropolis} ${b.details.name}`.toLowerCase();
    
    // Prioritize exact matches
    const aExactMatch = aText.includes(searchQuery.toLowerCase());
    const bExactMatch = bText.includes(searchQuery.toLowerCase());
    
    if (aExactMatch && !bExactMatch) return -1;
    if (!aExactMatch && bExactMatch) return 1;
    
    return 0;
  });

  // Update the grid with search results
  if (sortedResults.length > 0) {
    locatorsGrid.innerHTML = renderLocatorCards(sortedResults);
  } else {
    locatorsGrid.innerHTML = `
      <div style="
        grid-column: 1 / -1;
        text-align: center;
        padding: 40px;
        color: #aaa;
        font-size: 1.1em;
      ">
        No results found for "${searchQuery}". Try different keywords or check the spelling.
      </div>`;
  }
}

function showLocatorsOverlay() {
  let overlay = document.getElementById('locatorsOverlay');
  if (!overlay) {
    overlay = document.createElement('div');
    overlay.id = 'locatorsOverlay';
    overlay.className = 'locators-overlay';
    document.body.appendChild(overlay);
  }

  // Get unique categories and metropolises, with 'All' as the first option
  const categories = ['All', ...new Set(locatorsData.map(loc => loc.category))];
  const metropolises = ['All', ...new Set(locatorsData.map(loc => loc.metropolis))];

  // Get the currently selected metropolis from localStorage or default to 'Select City'
  const selectedMetropolis = localStorage.getItem('selectedMetropolis') || 'Select City';

  overlay.innerHTML = `
    <div class="locators-content">
      <div class="locators-header">
        <h2>Stores</h2>
        <div class="header-buttons-container">
          <button class="select-metropolis" onclick="showMetropolisModal()">
            <i class="fas fa-map-marker-alt"></i>
            <span class="metropolis-name">City</span>
          </button>
          <button class="close-locators" onclick="hideLocatorsOverlay()">
            <i class="fas fa-long-arrow-alt-left"></i>
          </button>
        </div>
      </div>
      
      <div class="locators-filter-container">
        <div class="locators-filter-buttons">
          ${categories.map(category => `
            <button 
              class="filter-button ${category === 'All' ? 'active' : ''}" 
              data-category="${category}" 
              onclick="filterLocators('${category}', 'category')"
            >
              ${category}
            </button>
          `).join('')}
        </div>
      </div>

      <div class="locators-grid" id="locatorsGrid">
        ${renderLocatorCards(locatorsData)}
      </div>
    </div>

    <div class="chat-container">
      <input type="text" id="exploreInput" placeholder="Search for services or locations..." />
      <div class="input-actions">
        <button class="send-message" id="exploreButton">
          <i class="fas fa-paper-plane"></i>
        </button>
      </div>
    </div>
  `;

  // Initialize search functionality
  const exploreInput = document.getElementById('exploreInput');
  const exploreButton = document.getElementById('exploreButton');

  // Debounced search for real-time filtering
  const debouncedSearch = debounce((query) => searchLocators(query), 300);

  // Event listeners
  exploreInput.addEventListener('input', (e) => {
    debouncedSearch(e.target.value);
  });

  exploreButton.addEventListener('click', () => {
    searchLocators(exploreInput.value);
  });

  // Handle Enter key
  exploreInput.addEventListener('keypress', (e) => {
    if (e.key === 'Enter') {
      searchLocators(exploreInput.value);
    }
  });

  setTimeout(() => overlay.classList.add('active'), 10);



  const style = document.createElement('style');
  style.textContent = `
  .locators-overlay {
  position: fixed;
  top: 60px;
  left: 0;
  right: 0;
  bottom: 60px;
  background: #1a1a1f;
  z-index: 1000;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
  overflow-y: auto;
  width: 100%;
  display: flex;
  flex-direction: column;
  scrollbar-width: none;
  -ms-overflow-style: none;
}

.locators-overlay::-webkit-scrollbar {
  display: none;
}

.locators-overlay.active {
  opacity: 1;
  visibility: visible;
}

.locators-content {
  flex: 1;
  width: 100%;
  max-width: 100%;
  padding: 20px;
  margin: 0 auto;
  position: relative;
}

.locators-header {
  padding: 8px 16px;
  background: rgba(26, 26, 31, 0.95);
  position: fixed;
  width: 100%;
  top: 0;
  left: 0;
  z-index: 30;
  border-bottom: 2px solid var(--primary-color);
  backdrop-filter: blur(10px);
  height: 65px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-top: 5px;
}

.locators-header h2 {
  color: var(--primary-color);
  margin: 0;
  font-size: 1.5em;
}

.header-buttons-container {
  display: flex;
  align-items: center;
  gap: 12px;
}

.select-metropolis {
  background: rgba(255, 215, 0, 0.1);
  color: #e6e6e6;
  border: none;
  padding: 10px 15px;
  border-radius: 20px;
  cursor: pointer;
  display: flex;
  align-items: center;
  gap: 10px;
  transition: all 0.3s ease;
}

.select-metropolis:hover {
  background: #ffd700;
  color: #1a1a1f;
  transform: scale(1.05);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.close-locators {
  background: none;
  border: none;
  color: var(--primary-color);
  font-size: 1.5em;
  cursor: pointer;
  padding: 5px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-left: 0px;
}

.locators-filter-container {
  position: fixed;
  top: 70px;
  left: 0;
  width: 100vw;
  max-width: 100vw;
  z-index: 10;
  background: #1a1a1f;
  margin-left: 10px;
  padding: 10px 15px;
  box-sizing: border-box;
}

.locators-filter-buttons {
  display: flex;
  justify-content: flex-start;
  gap: 4px;
  padding-bottom: 10px;
  width: 100vw;
  margin-left: calc(-50vw + 50%);
  overflow-x: auto;
  scrollbar-width: none;
}

.locators-filter-buttons::-webkit-scrollbar {
  height: 0px;
}

.locators-filter-buttons::-webkit-scrollbar-thumb {
  background-color: var(--primary-color);
  border-radius: 3px;
}

.filter-button {
  margin-top: 2px;
  margin-left: 2px;
  margin-right: 5px;
  flex-shrink: 0;
  background: rgba(255, 215, 0, 0.1);
  color: var(--text-light);
  border: 1px solid rgba(255, 215, 0, 0.2);
  padding: 10px 15px;
  border-radius: 25px;
  transition: all 0.3s ease;
  cursor: pointer;
  white-space: nowrap;
  font-weight: 500;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
}

.filter-button:hover {
  background: var(--primary-color);
  color: black;
  transform: scale(1.05);
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2);
}

.filter-button.active {
  background: var(--primary-color);
  color: black;
  font-weight: 700;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.3);
}

.locators-grid-container {
  flex: 1;
  width: 100%;
  padding-bottom: 20px;
  position: relative;
}

.locators-grid {
  margin-top: 70px;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
  gap: 20px;
  animation: fadeInUp 0.5s ease-out;
  padding-bottom: 140px;
  width: 100%;
}

.locator-card {
  background: rgba(255, 255, 255, 0.05);
  border-radius: 16px;
  overflow: hidden;
  transition: all 0.3s ease;
  border: 1px solid rgba(255, 255, 255, 0.1);
  cursor: pointer;
}

.locator-card:hover {
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.2);
  border-color: rgba(255, 215, 0, 0.3);
}

.locator-card-header {
  display: flex;
  align-items: center;
  gap: 15px;
  padding: 20px;
  background: rgba(255, 255, 255, 0.03);
  border-bottom: 1px solid rgba(255, 255, 255, 0.05);
}

.brand-logo {
  width: 60px;
  height: 60px;
  border-radius: 12px;
  object-fit: cover;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.locator-card-title {
  flex: 1;
}

.locator-card-title h3 {
  margin: 0;
  font-size: 1.2em;
  color: #fff;
  font-weight: 600;
}

.category-tag {
  margin: 5px 0 0;
  font-size: 0.9em;
  color: rgba(255, 215, 0, 0.8);
  font-weight: 500;
}

.locator-card-body {
  padding: 20px;
}

.locator-description {
  margin: 0;
  font-size: 0.95em;
  color: rgba(255, 255, 255, 0.8);
  line-height: 1.5;
}

.locator-card-actions {
  display: flex;
  gap: 10px;
  padding: 15px 20px;
  background: rgba(255, 255, 255, 0.03);
  border-top: 1px solid rgba(255, 255, 255, 0.05);
}

.action-button {
  flex: 1;
  background: rgba(255, 215, 0, 0.1);
  border: none;
  border-radius: 8px;
  padding: 10px;
  color: #fff;
  cursor: pointer;
  transition: all 0.3s ease;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 8px;
  font-size: 0.9em;
}

.action-button:hover {
  background: rgba(255, 215, 0, 0.2);
  transform: translateY(-2px);
}

.action-button i {
  font-size: 1.1em;
}

/* Responsive Design */
@media (max-width: 768px) {
  .locator-card-header {
    padding: 15px;
  }

  .brand-logo {
    width: 50px;
    height: 50px;
  }

  .locator-card-title h3 {
    font-size: 1.1em;
  }

  .locator-card-body {
    padding: 15px;
  }

  .locator-card-actions {
    padding: 10px 15px;
    flex-wrap: wrap;
  }

  .action-button {
    flex: 1 1 45%;
    padding: 8px;
    font-size: 0.85em;
  }
}

.chat-container {
  position: fixed;
  bottom: 60px;
  left: 0;
  right: 0;
  width: 100%;
  max-width: 100%;
  z-index: 1000;
  padding: 20px;
  background: #1a1a1f;
  border-top: 1px solid rgba(255, 215, 0, 0.1);
  display: flex;
  gap: 12px;
  align-items: center;
  box-sizing: border-box;
}

#exploreInput {
  flex: 1;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 215, 0, 0.2);
  border-radius: 12px;
  padding: 20px;
  color: var(--text-light);
  font-size: 0.95em;
  width: 100%;
}

/* Desktop and laptop styles */
@media (min-width: 769px) {
  .chat-container {
    width: 100%;
    display: flex;
    justify-content: center;
  }
  
  #exploreInput {
    width: 60%;
    max-width: 1200px;
  }
  
  .locators-grid {
    padding-bottom: 180px;
  }
}

/* Mobile styles */
@media (max-width: 768px) {
  .chat-container {
    width: 100%;
    left: 0;
    transform: none;
    padding: 10px;
    gap: 8px;
  }

  .locators-grid {
    grid-template-columns: 1fr;
    padding: 0 10px;
    margin-top: 80px;
    gap: 15px;
  }

  .locator-card {
    width: 100%;
    margin: 0;
  }

  .locators-grid-container {
    width: 100%;
    max-width: 100%;
    padding: 0;
  }

  .locators-content {
    padding: 10px 0;
    padding-bottom: 200px;
  }

  #exploreInput {
    width: 100%;
    padding: 20px 20px;
  }
}
   `;
  document.head.appendChild(style);
}

// Function to get category-specific content
function getCategorySpecificContent(locator) {
  switch (locator.category) {
    case 'Grocery':
      return `
        <div class="category-specific">
          <h3>Featured Products</h3>
          <div class="product-list">
            ${locator.details.menu?.map(item => `
              <div class="product-item">
                <h4>${item.name}</h4>
                <p>${item.price}</p>
              </div>
            `).join('') || ''}
          </div>
        </div>
      `;

    case 'Bakery':
      return `
        <div class="category-specific">
          <h3>Today's Specials</h3>
          <div class="menu-grid">
            ${locator.details.menu?.map(item => `
              <div class="menu-item">
                <h4>${item.name}</h4>
                <p class="price">${item.price}</p>
              </div>
            `).join('') || ''}
          </div>
        </div>
      `;

    case 'Garden Supplies':
      return `
        <div class="category-specific">
          <h3>Services</h3>
          <div class="services-list">
            <div class="service-item">
              <h4>Consultations</h4>
              <p>Expert advice on plant care and garden design</p>
            </div>
            <div class="service-item">
              <h4>Delivery</h4>
              <p>Free delivery for orders above $50</p>
            </div>
          </div>
        </div>
      `;

    default:
      return '';
  }
}

// Function to close details page
function closeLocatorDetails() {
  const detailsPage = document.querySelector('.locator-details-page');
  if (detailsPage) {
    detailsPage.style.transform = 'translateX(100%)';
    setTimeout(() => detailsPage.remove(), 300);
  }
}

// Carousel functions
let currentSlideIndex = 1;

function changeSlide(n) {
  showSlides(currentSlideIndex += n);
}

function currentSlide(n) {
  showSlides(currentSlideIndex = n);
}

function showSlides(n) {
  const dots = document.getElementsByClassName("dot");
  if (n > dots.length) currentSlideIndex = 1;
  if (n < 1) currentSlideIndex = dots.length;

  // Update dots
  for (let i = 0; i < dots.length; i++) {
    dots[i].className = dots[i].className.replace(" active", "");
  }
  dots[currentSlideIndex-1].className += " active";
}

// Share function
function shareLocation(name) {
  if (navigator.share) {
    navigator.share({
      title: name,
      text: `Check out ${name} on our platform!`,
      url: window.location.href
    }).catch(console.error);
  } else {
    // Fallback
    const dummy = document.createElement('input');
    document.body.appendChild(dummy);
    dummy.value = window.location.href;
    dummy.select();
    document.execCommand('copy');
    document.body.removeChild(dummy);
    
    alert('Link copied to clipboard!');
  }
}

function renderLocatorCards(filteredData) {
  return filteredData.map(locator => `
    <div class="locator-card" onclick="openStorePage('${locator.category}')">
      <div class="locator-card-header">
        <img src="${locator.details.image}" alt="${locator.details.name}" class="brand-logo">
        <div class="locator-card-title">
          <h3>${locator.details.name}</h3>
          <p class="category-tag">${locator.category}</p>
        </div>
      </div>
      <div class="locator-card-body">
        <p class="locator-description">${locator.details.description}</p>
      </div>
      <div class="locator-card-actions">
        ${locator.details.menu ? `
          <a href="${locator.details.menuLink}" target="_blank" class="action-button" onclick="event.stopPropagation()">
            <i class="fas fa-utensils"></i> Menu
          </a>
        ` : ''}
        <a href="${locator.details.mapLink}" target="_blank" class="action-button" onclick="event.stopPropagation()">
          <i class="fas fa-map-marker-alt"></i> Map
        </a>
        <button class="action-button" onclick="openStorePage('${locator.category}'); event.stopPropagation()">
          <i class="fas fa-info-circle"></i> Info
        </button>
        <button class="action-button chat-button" onclick="showChatSupport('${locator.category}'); event.stopPropagation()">
          <i class="fas fa-comments"></i> Chat
        </button>
      </div>
    </div>
  `).join('');
}

function openStorePage(category) {
  const selectedMetropolis = localStorage.getItem('selectedMetropolis') || 'Select City';
  const locator = locatorsData.find(loc => loc.category === category);
  if (!locator) return;

  // Filter outlets based on the selected metropolis
  const filteredOutlets = locator.details.outlets.filter(outlet => {
    return outlet.address.includes(selectedMetropolis);
  });

  const storePage = document.createElement('div');
  storePage.className = 'store-page';
  storePage.innerHTML = `
    <div class="store-header">
      <button class="back-button" onclick="closeStorePage()">
        <i class="fas fa-arrow-left"></i> Back
      </button>
      <h2>${locator.details.name}</h2>
    </div>
    <div class="store-content">
      <!-- Store Info -->
      <div class="store-info">
        <img src="${locator.details.image}" alt="${locator.details.name}" class="store-logo">
        <h3>${locator.details.name}</h3>
        <p class="store-description">${locator.details.description}</p>
        <div class="social-media">
          <a href="${locator.details.social?.facebook}" target="_blank"><i class="fab fa-facebook"></i></a>
          <a href="${locator.details.social?.twitter}" target="_blank"><i class="fab fa-twitter"></i></a>
          <a href="${locator.details.social?.instagram}" target="_blank"><i class="fab fa-instagram"></i></a>
        </div>
      </div>
      
      <!-- Tabs -->
      <div class="store-tabs">
        <button class="tab-button active" data-tab="locator">Store Locator</button>
        <button class="tab-button" data-tab="catalog">Product Catalog</button>
        <button class="tab-button" data-tab="promos">Promos & Deals</button>
        <button class="tab-button" data-tab="support">Customer Support</button>
      </div>
      
      <!-- Tab Content -->
      <div class="tab-content">
        <div id="locator" class="tab-pane active">
          <!-- Store Locator Content -->
          <div class="store-locator">
            <h4>Find Stores in ${selectedMetropolis}</h4>
            <div class="locator-grid" id="locatorGrid">
              ${renderOutlets(filteredOutlets)}
            </div>
          </div>
        </div>
        <div id="catalog" class="tab-pane">
          <!-- Product Catalog Content -->
          <div class="product-catalog">
            <h4>Available Products</h4>
            <div class="product-grid" id="productGrid">
              ${locator.details.menu?.map(item => `
                <div class="product-item">
                  <img src="${item.image}" alt="${item.name}">
                  <h5>${item.name}</h5>
                  <p>${item.price}</p>
                  <button class="add-to-cart" onclick="addToCart('${item.name}', '${item.price}')">
                    <i class="fas fa-cart-plus"></i> Add to Cart
                  </button>
                </div>
              `).join('')}
            </div>
          </div>
        </div>
        <div id="promos" class="tab-pane">
          <!-- Promos & Deals Content -->
          <div class="promos-deals" id="promosGrid">
            <h4>Available Promos & Deals</h4>
            ${locator.details.promos?.map(promo => `
              <div class="promo-item">
                <p>${promo.code} - ${promo.description}</p>
                <button onclick="copyPromo('${promo.code}')">Copy Code</button>
              </div>
            `).join('')}
          </div>
        </div>
        <div id="support" class="tab-pane">
          <!-- Customer Support Content -->
          <div class="customer-support" id="supportContent">
            <h4>Contact Support</h4>
            <p>Email: ${locator.details.support?.email}</p>
            <p>Phone: ${locator.details.support?.phone}</p>
            <button onclick="showChatSupport('${locator.category}')">
              <i class="fas fa-comments"></i> Chat with Us
            </button>
          </div>
        </div>
      </div>
      
      <!-- Search Container -->
      <div class="chat-container">
        <input type="text" id="storeInput" placeholder="Search for services, products, or locations..." />
        <div class="input-actions">
          <button class="send-message" id="storeButton">
            <i class="fas fa-paper-plane"></i>
          </button>
        </div>
      </div>
    </div>
  `;

  document.body.appendChild(storePage);
  addStorePageStyles();
  initializeTabs();
  initializeSearch();
  scrollToTop();
}

function renderOutlets(outlets) {
  return outlets.map(outlet => `
    <div class="outlet-card">
      <h5>${outlet.name}</h5>
      <p>${outlet.address}</p>
      <p>${outlet.timings}</p>
      <a href="${outlet.mapLink}" target="_blank" class="action-button">
        <i class="fas fa-map-marker-alt"></i> View on Map
      </a>
    </div>
  `).join('');
}

// Function to scroll to the top of the store page
function scrollToTop() {
  const storeContent = document.querySelector('.store-content');
  if (storeContent) {
    storeContent.scrollTo({ top: 0, behavior: 'smooth' });
  }
}

// Function to initialize search functionality with debounce
function initializeSearch() {
  const storeInput = document.getElementById('storeInput');
  if (storeInput) {
    storeInput.addEventListener('input', debounce((e) => {
      const searchTerm = e.target.value.toLowerCase().trim();
      const intent = understandUserIntent(searchTerm);
      filterStoreContent(searchTerm, intent);
    }, 300));
  }
}

// Function to understand user intent using simple NLP
function understandUserIntent(searchTerm) {
  if (searchTerm.includes('offer') || searchTerm.includes('deal')) {
    return 'promos';
  } else if (searchTerm.includes('product') || searchTerm.includes('item')) {
    return 'catalog';
  } else if (searchTerm.includes('support') || searchTerm.includes('contact')) {
    return 'support';
  } else if (searchTerm.includes('store') || searchTerm.includes('location')) {
    return 'locator';
  }
  return null;
}

// Function to filter store content based on search term and intent
function filterStoreContent(searchTerm, intent) {
  const storeContent = document.querySelector('.store-content');
  const tabPanes = document.querySelectorAll('.tab-pane');
  const noResultsMessage = document.getElementById('noResultsMessage');

  if (!searchTerm) {
    // If search term is empty, show all content
    tabPanes.forEach(pane => pane.style.display = 'block');
    if (noResultsMessage) noResultsMessage.remove();
    return;
  }

  // Hide all tab panes initially
  tabPanes.forEach(pane => pane.style.display = 'none');

  // Switch to the relevant tab based on intent
  if (intent) {
    document.querySelector(`[data-tab="${intent}"]`).click();
  }

  // Filter Product Catalog
  const productGrid = document.getElementById('productGrid');
  if (productGrid) {
    const products = productGrid.querySelectorAll('.product-item');
    let productMatch = false;
    products.forEach(product => {
      const productName = product.querySelector('h5').textContent.toLowerCase();
      const productDescription = product.querySelector('p').textContent.toLowerCase();
      if (productName.includes(searchTerm) || productDescription.includes(searchTerm)) {
        product.style.display = 'block';
        productMatch = true;
      } else {
        product.style.display = 'none';
      }
    });
    if (productMatch) {
      document.getElementById('catalog').style.display = 'block';
    }
  }

  // Filter Promos & Deals
  const promosGrid = document.getElementById('promosGrid');
  if (promosGrid) {
    const promos = promosGrid.querySelectorAll('.promo-item');
    let promoMatch = false;
    promos.forEach(promo => {
      const promoText = promo.textContent.toLowerCase();
      if (promoText.includes(searchTerm)) {
        promo.style.display = 'flex';
        promoMatch = true;
      } else {
        promo.style.display = 'none';
      }
    });
    if (promoMatch) {
      document.getElementById('promos').style.display = 'block';
    }
  }

  // Filter Customer Support
  const supportContent = document.getElementById('supportContent');
  if (supportContent) {
    const supportText = supportContent.textContent.toLowerCase();
    if (supportText.includes(searchTerm)) {
      document.getElementById('support').style.display = 'block';
    }
  }

  // Filter Store Locator
  const locatorGrid = document.getElementById('locatorGrid');
  if (locatorGrid) {
    const locators = locatorGrid.querySelectorAll('.locator-card');
    let locatorMatch = false;
    locators.forEach(locator => {
      const locatorText = locator.textContent.toLowerCase();
      if (locatorText.includes(searchTerm)) {
        locator.style.display = 'block';
        locatorMatch = true;
      } else {
        locator.style.display = 'none';
      }
    });
    if (locatorMatch) {
      document.getElementById('locator').style.display = 'block';
    }
  }

  // Show no results message if no matches found
  if (!productMatch && !promoMatch && !supportText?.includes(searchTerm) && !locatorMatch) {
    if (!noResultsMessage) {
      const noResultsDiv = document.createElement('div');
      noResultsDiv.id = 'noResultsMessage';
      noResultsDiv.textContent = 'No results found.';
      noResultsDiv.style.textAlign = 'center';
      noResultsDiv.style.color = 'rgba(255, 255, 255, 0.8)';
      noResultsDiv.style.marginTop = '20px';
      storeContent.appendChild(noResultsDiv);
    }
  } else {
    if (noResultsMessage) noResultsMessage.remove();
  }

  // Scroll to the top of the store page
  scrollToTop();
}

// Function to close the store page
function closeStorePage() {
  const storePage = document.querySelector('.store-page');
  if (storePage) {
    storePage.remove();
  }
}

// Function to initialize tabs on the store page
function initializeTabs() {
  const tabButtons = document.querySelectorAll('.tab-button');
  const tabPanes = document.querySelectorAll('.tab-pane');

  tabButtons.forEach(button => {
    button.addEventListener('click', () => {
      const tabName = button.getAttribute('data-tab');
      tabButtons.forEach(btn => btn.classList.remove('active'));
      tabPanes.forEach(pane => pane.classList.remove('active'));
      button.classList.add('active');
      document.getElementById(tabName).classList.add('active');
    });
  });
}

function addStorePageStyles() {
  const style = document.createElement('style');
  style.textContent = `
    /* Store Page Container */
    .store-page {
      position: fixed;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      background: #1a1a1f;
      z-index: 2000;
      overflow-y: auto;
      padding: 20px;
      box-sizing: border-box;
      font-family: 'Inter', sans-serif;
    }

    /* Store Header */
    .store-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 20px;
      padding: 15px;
      background: rgba(255, 255, 255, 0.05);
      border-radius: 16px;
      backdrop-filter: blur(10px);
    }

    .back-button {
      background: none;
      border: none;
      color: #fff;
      font-size: 1.5em;
      cursor: pointer;
      transition: transform 0.2s ease, opacity 0.2s ease;
    }

    .back-button:hover {
      transform: scale(1.1);
      opacity: 0.8;
    }

    .store-header h2 {
      margin: 0;
      font-size: 1.5em;
      color: #fff;
      font-weight: 600;
      letter-spacing: -0.5px;
    }

    /* Store Info */
    .store-info {
      text-align: center;
      margin-bottom: 20px;
    }

    .store-logo {
      width: 100px;
      height: 100px;
      border-radius: 50%;
      object-fit: cover;
      border: 3px solid rgba(255, 215, 0, 0.5);
      margin-bottom: 15px;
      transition: transform 0.3s ease;
    }

    .store-logo:hover {
      transform: scale(1.05);
    }

    .store-info h3 {
      margin: 0;
      font-size: 1.75em;
      color: #fff;
      font-weight: 600;
      letter-spacing: -0.5px;
    }

    .store-description {
      color: rgba(255, 255, 255, 0.8);
      font-size: 1em;
      margin-top: 10px;
      line-height: 1.5;
    }

    /* Social Media Icons */
    .social-media {
      display: flex;
      justify-content: center;
      gap: 20px;
      margin-top: 20px;
    }

    .social-media a {
      color: #fff;
      font-size: 1.75em;
      transition: transform 0.3s ease, color 0.3s ease;
    }

    .social-media a:hover {
      color: #ffd700;
      transform: scale(1.2);
    }

    /* Tabs */
    .store-tabs {
      display: flex;
      justify-content: space-around;
      margin-bottom: 20px;
      background: rgba(255, 255, 255, 0.05);
      border-radius: 16px;
      padding: 10px;
      backdrop-filter: blur(10px);
    }

    .tab-button {
      background: none;
      border: none;
      color: rgba(255, 255, 255, 0.7);
      font-size: 1em;
      cursor: pointer;
      padding: 12px 24px;
      border-radius: 12px;
      transition: all 0.3s ease;
    }

    .tab-button.active {
      background: rgba(255, 215, 0, 0.1);
      color: #ffd700;
      font-weight: 600;
    }

    .tab-button:hover {
      background: rgba(255, 215, 0, 0.1);
    }

    /* Tab Content */
    .tab-content {
      padding-bottom: 200px;
    }

    .tab-pane {
      display: none;
      animation: fadeIn 0.5s ease;
    }

    .tab-pane.active {
      display: block;
    }

    @keyframes fadeIn {
      from { opacity: 0; }
      to { opacity: 1; }
    }

    /* Product Catalog */
    .product-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(180px, 1fr));
      gap: 20px;
    }

    .product-item {
      background: rgba(255, 255, 255, 0.05);
      border-radius: 16px;
      padding: 20px;
      text-align: center;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      backdrop-filter: blur(10px);
    }

    .product-item:hover {
      transform: translateY(-5px);
      box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
    }

    .product-item img {
      width: 100%;
      height: auto;
      border-radius: 12px;
      margin-bottom: 15px;
      transition: transform 0.3s ease;
    }

    .product-item:hover img {
      transform: scale(1.05);
    }

    .product-item h5 {
      margin: 0;
      font-size: 1.1em;
      color: #fff;
      font-weight: 600;
    }

    .product-item p {
      margin: 10px 0;
      color: rgba(255, 255, 255, 0.8);
      font-size: 0.95em;
    }

    .add-to-cart {
      background: rgba(255, 215, 0, 0.1);
      border: none;
      color: #fff;
      padding: 10px 20px;
      border-radius: 12px;
      cursor: pointer;
      transition: background 0.3s ease, transform 0.3s ease;
    }

    .add-to-cart:hover {
      background: rgba(255, 215, 0, 0.2);
      transform: scale(1.05);
    }

    /* Promos & Deals */
    .promos-deals {
      display: grid;
      gap: 20px;
    }

    .promo-item {
      background: rgba(255, 255, 255, 0.05);
      border-radius: 16px;
      padding: 20px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      backdrop-filter: blur(10px);
    }

    .promo-item p {
      margin: 0;
      color: rgba(255, 255, 255, 0.8);
      font-size: 1em;
    }

    .promo-item button {
      background: rgba(255, 215, 0, 0.1);
      border: none;
      color: #fff;
      padding: 10px 20px;
      border-radius: 12px;
      cursor: pointer;
      transition: background 0.3s ease, transform 0.3s ease;
    }

    .promo-item button:hover {
      background: rgba(255, 215, 0, 0.2);
      transform: scale(1.05);
    }

    /* Customer Support */
    .customer-support {
      text-align: center;
      padding: 20px;
      background: rgba(255, 255, 255, 0.05);
      border-radius: 16px;
      backdrop-filter: blur(10px);
    }

    .customer-support p {
      margin: 10px 0;
      color: rgba(255, 255, 255, 0.8);
      font-size: 1em;
    }

    .customer-support button {
      background: rgba(255, 215, 0, 0.1);
      border: none;
      color: #fff;
      padding: 12px 24px;
      border-radius: 12px;
      cursor: pointer;
      transition: background 0.3s ease, transform 0.3s ease;
    }

    .customer-support button:hover {
      background: rgba(255, 215, 0, 0.2);
      transform: scale(1.05);
    }

    /* Chat Container */
    .chat-container {
      position: fixed;
      bottom: 0;
      left: 0;
      right: 0;
      width: 100%;
      max-width: 100%;
      z-index: 1000;
      padding: 20px;
      background: #1a1a1f;
      border-top: 1px solid rgba(255, 215, 0, 0.1);
      display: flex;
      gap: 12px;
      align-items: center;
      box-sizing: border-box;
      backdrop-filter: blur(10px);
    }

    #storeInput {
      flex: 1;
      background: rgba(255, 255, 255, 0.05);
      border: 1px solid rgba(255, 215, 0, 0.2);
      border-radius: 12px;
      padding: 20px;
      color: #fff;
      font-size: 1em;
      width: 100%;
      transition: border-color 0.3s ease;
    }

    #storeInput:focus {
      border-color: rgba(255, 215, 0, 0.5);
    }

        /* Outlet Card Styles */
    .outlet-card {
      background: rgba(255, 255, 255, 0.05);
      border-radius: 16px;
      padding: 20px;
      margin-bottom: 20px;
      transition: transform 0.3s ease, box-shadow 0.3s ease;
      backdrop-filter: blur(10px);
    }

    .outlet-card:hover {
      transform: translateY(-5px);
      box-shadow: 0 8px 25px rgba(0, 0, 0, 0.3);
    }

    .outlet-card h5 {
      margin: 0;
      font-size: 1.1em;
      color: #fff;
      font-weight: 600;
    }

    .outlet-card p {
      margin: 10px 0;
      color: rgba(255, 255, 255, 0.8);
      font-size: 0.95em;
    }

    .outlet-card .action-button {
      background: rgba(255, 215, 0, 0.1);
      border: none;
      color: #fff;
      padding: 10px 20px;
      border-radius: 12px;
      cursor: pointer;
      transition: background 0.3s ease, transform 0.3s ease;
      display: inline-block;
      margin-top: 10px;
    }

    .outlet-card .action-button:hover {
      background: rgba(255, 215, 0, 0.2);
      transform: scale(1.05);
    }

    /* Responsive Design */
    @media (max-width: 768px) {
      .store-header h2 {
        font-size: 1.2em;
      }

      .store-logo {
        width: 80px;
        height: 80px;
      }

      .store-description {
        font-size: 0.9em;
      }

      .tab-button {
        font-size: 0.9em;
        padding: 10px 20px;
      }

      .product-grid {
        grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
      }

      .product-item h5 {
        font-size: 1em;
      }

      .product-item p {
        font-size: 0.85em;
      }

      .add-to-cart {
        font-size: 0.85em;
      }

      .promo-item p {
        font-size: 0.9em;
      }

      .promo-item button {
        font-size: 0.85em;
      }

      .customer-support button {
        font-size: 0.9em;
      }
    }

    /* Small Mobile Optimizations */
    @media (max-width: 480px) {
      .store-page {
        padding: 10px;
      }

      .product-grid {
        grid-template-columns: repeat(auto-fit, minmax(120px, 1fr));
        gap: 10px;
      }

      .tab-button {
        padding: 8px 16px;
        font-size: 0.85em;
      }

      .chat-container {
        padding: 20px;
      }

      #storeInput {
        padding: 20px;
      }
    }
  `;
  document.head.appendChild(style);
}

function showMetropolisModal() {
  // Enhanced data processing with more robust error handling
  const metropolisGroups = locatorsData.reduce((acc, locator) => {
    if (!locator || !locator.metropolis) return acc;
    
    const metropolis = locator.metropolis.trim();
    if (!metropolis) return acc;

    if (!acc[metropolis]) {
      acc[metropolis] = {
        name: metropolis,
        categories: new Set(),
        count: 0,
        uniqueCategories: new Set() // Track unique categories more precisely
      };
    }
    
    // Only add if category is unique for this metropolis
    if (locator.category && !acc[metropolis].uniqueCategories.has(locator.category)) {
      acc[metropolis].categories.add(locator.category);
      acc[metropolis].uniqueCategories.add(locator.category);
    }
    acc[metropolis].count++;
    return acc;
  }, {});

  // More sophisticated sorting with secondary criteria
  const metropoliesToShow = Object.values(metropolisGroups)
    .sort((a, b) => {
      // Primary sort by number of locations
      if (b.count !== a.count) return b.count - a.count;
      
      // Secondary sort by number of unique categories
      return b.categories.size - a.categories.size;
    });

  const modal = document.createElement('div');
  modal.id = 'metropolisSelectionModal';
  modal.setAttribute('role', 'dialog');
  modal.setAttribute('aria-labelledby', 'metropolis-modal-title');
  modal.className = 'metropolis-selection-modal';
  
  modal.innerHTML = `
    <div class="metropolis-modal-content" role="document">
      <div class="metropolis-modal-header">
        <h2 id="metropolis-modal-title">Select Your City</h2>
        <p>Explore services across different metropolises</p>
      </div>
      
      <div class="metropolis-grid" id="metropolisGrid">
        ${metropoliesToShow.map(metropolis => `
          <div 
            class="metropolis-card" 
            onclick="selectMetropolis('${metropolis.name}')"
            onkeydown="handleMetropolisKeydown(event, '${metropolis.name}')"
            tabindex="0"
            role="button"
            aria-label="Select ${metropolis.name}"
          >
            <div class="metropolis-card-inner">
              <div class="metropolis-icon">
                <i class="fas fa-city" aria-hidden="true"></i>
              </div>
              <div class="metropolis-details">
                <h3>${metropolis.name}</h3>
                <div class="metropolis-meta">
                  <span class="locations-count">
                    ${metropolis.count} Location${metropolis.count !== 1 ? 's' : ''}
                  </span>
                </div>
              </div>
              <div class="metropolis-select-icon" aria-hidden="true">
                <i class="fas fa-chevron-right"></i>
              </div>
            </div>
          </div>
        `).join('')}
      </div>

      <div class="metropolis-modal-footer">
        <button 
          onclick="closeMetropolisModal()" 
          class="close-metropolis-modal"
          aria-label="Close City Selection Modal"
        >
          Close
        </button>
      </div>
    </div>
  `;
  
  // Add styles
const style = document.createElement('style');
style.textContent = `
/* Modal Base */
.metropolis-selection-modal {
  position: fixed;
  inset: 0;
  background: rgba(17, 17, 23, 0.98);
  z-index: 1500;
  display: flex;
  align-items: center;
  justify-content: center;
  backdrop-filter: blur(8px);
  animation: modalFadeIn 0.25s ease-out;
  overscroll-behavior: contain;
  padding: 1rem;
}

/* Modal Content Container */
.metropolis-modal-content {
  width: 100%;
  max-width: 900px;
  background: linear-gradient(145deg, #1e1e24, #2a2a35);
  border-radius: 1.25rem;
  box-shadow: 
    0 25px 50px -12px rgba(0, 0, 0, 0.4),
    0 0 0 1px rgba(255, 255, 255, 0.05);
  padding: 2rem;
  max-height: 85vh;
  overflow-y: auto;
  position: relative;
  transform: translateY(0);
  transition: transform 0.3s ease;
  scrollbar-width: thin;
  scrollbar-color: rgba(255, 215, 0, 0.3) transparent;
}

.metropolis-modal-content:hover {
  transform: translateY(-2px);
}

/* Header Styling */
.metropolis-modal-header {
  text-align: left;
  margin-bottom: 2rem;
  padding-bottom: 1.5rem;
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
}

.metropolis-modal-header h2 {
  font-size: 1.75rem;
  font-weight: 600;
  color: #ffffff;
  margin-bottom: 0.75rem;
  letter-spacing: -0.02em;
  line-height: 1.2;
}

.metropolis-modal-header p {
  color: rgba(255, 255, 255, 0.7);
  font-size: 1rem;
  line-height: 1.5;
  max-width: 600px;
}

/* Grid Layout */
.metropolis-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
  gap: 1.25rem;
  margin-bottom: 2rem;
}

/* Card Styling */
.metropolis-card {
  background: rgba(255, 255, 255, 0.03);
  border-radius: 1rem;
  transition: all 0.2s ease;
  border: 1px solid rgba(255, 255, 255, 0.08);
  position: relative;
  overflow: hidden;
}

.metropolis-card:hover {
  transform: translateY(-4px);
  background: rgba(255, 255, 255, 0.05);
  border-color: rgba(255, 215, 0, 0.3);
  box-shadow: 
    0 12px 20px -8px rgba(0, 0, 0, 0.3),
    0 0 0 1px rgba(255, 215, 0, 0.2);
}

.metropolis-card-inner {
  display: flex;
  align-items: center;
  padding: 1.25rem;
  gap: 1rem;
}

/* Icon Container */
.metropolis-icon {
  background: rgba(255, 215, 0, 0.08);
  width: 3.5rem;
  height: 3.5rem;
  border-radius: 0.75rem;
  display: flex;
  align-items: center;
  justify-content: center;
  color: #ffd700;
  font-size: 1.25rem;
  flex-shrink: 0;
  transition: all 0.2s ease;
}

.metropolis-card:hover .metropolis-icon {
  background: rgba(255, 215, 0, 0.15);
  transform: scale(1.05);
}

/* Content Details */
.metropolis-details {
  flex-grow: 1;
}

.metropolis-details h3 {
  color: #ffffff;
  font-size: 1.125rem;
  font-weight: 500;
  margin-bottom: 0.5rem;
  line-height: 1.3;
}

.metropolis-meta {
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
  font-size: 0.875rem;
}

.locations-count {
  color: rgba(255, 215, 0, 0.9);
  font-weight: 500;
}

/* Footer Styling */
.metropolis-modal-footer {
  margin-top: 2rem;
  padding-top: 1.5rem;
  border-top: 1px solid rgba(255, 255, 255, 0.1);
  text-align: right;
}

.close-metropolis-modal {
  background: rgba(255, 215, 0, 0.1);
  color: #ffffff;
  border: 1px solid rgba(255, 215, 0, 0.2);
  padding: 0.75rem 1.5rem;
  border-radius: 0.75rem;
  font-size: 0.875rem;
  font-weight: 500;
  cursor: pointer;
  transition: all 0.2s ease;
}

.close-metropolis-modal:hover {
  background: #ffd700;
  color: #000000;
  transform: translateY(-2px);
  box-shadow: 0 4px 12px rgba(255, 215, 0, 0.2);
}

/* Animations */
@keyframes modalFadeIn {
  from {
    opacity: 0;
    transform: scale(0.98);
  }
  to {
    opacity: 1;
    transform: scale(1);
  }
}

/* Scrollbar Styling */
.metropolis-modal-content::-webkit-scrollbar {
  width: 8px;
}

.metropolis-modal-content::-webkit-scrollbar-track {
  background: transparent;
}

.metropolis-modal-content::-webkit-scrollbar-thumb {
  background: rgba(255, 215, 0, 0.3);
  border-radius: 4px;
}

/* Responsive Design */
@media (max-width: 768px) {
  .metropolis-selection-modal {
    padding: 0.75rem;
  }

  .metropolis-modal-content {
    padding: 1.5rem;
    max-height: 90vh;
  }

  .metropolis-modal-header {
    margin-bottom: 1.5rem;
    padding-bottom: 1rem;
  }

  .metropolis-modal-header h2 {
    font-size: 1.5rem;
  }

  .metropolis-grid {
    gap: 1rem;
  }

  .metropolis-card-inner {
    padding: 1rem;
  }

  .metropolis-icon {
    width: 3rem;
    height: 3rem;
  }
}

@media (max-width: 480px) {
  .metropolis-modal-content {
    padding: 1.25rem;
  }

  .metropolis-grid {
    grid-template-columns: 1fr;
  }

  .metropolis-modal-header h2 {
    font-size: 1.25rem;
  }
}
  `;
document.head.appendChild(style);
document.body.appendChild(modal);


  // Add keyboard trap and focus management
  const firstFocusableElement = modal.querySelector('.metropolis-card');
  const lastFocusableElement = modal.querySelector('.close-metropolis-modal');

  modal.addEventListener('keydown', (e) => {
    if (e.key === 'Escape') {
      closeMetropolisModal();
    }

    // Keyboard trap
    if (e.key === 'Tab') {
      if (e.shiftKey && document.activeElement === firstFocusableElement) {
        lastFocusableElement.focus();
        e.preventDefault();
      } else if (!e.shiftKey && document.activeElement === lastFocusableElement) {
        firstFocusableElement.focus();
        e.preventDefault();
      }
    }
  });

  // Focus the first metropolis card when modal opens
  firstFocusableElement?.focus();
}

function handleMetropolisKeydown(event, metropolis) {
  // Allow selection via keyboard
  if (event.key === 'Enter' || event.key === ' ') {
    selectMetropolis(metropolis);
  }
}

// Update the selectMetropolis function to update the button text
function selectMetropolis(metropolis) {
    if (!metropolis) return;
    
    // Store the selected metropolis
    localStorage.setItem('selectedMetropolis', metropolis);
    
    // Update the button text and style
    const metropolisButton = document.querySelector('.select-metropolis');
    if (metropolisButton) {
        const nameSpan = metropolisButton.querySelector('.metropolis-name');
        if (nameSpan) {
            nameSpan.textContent = metropolis;
        }
        metropolisButton.classList.add('has-selection');
    }
    
    // Close the modal with animation
    closeMetropolisModal();
    
    // Filter locators by selected metropolis
    const filteredData = locatorsData.filter(loc => 
        loc && loc.metropolis && loc.metropolis.trim() === metropolis
    );
    
    // Update the grid with filtered locators
    const locatorsGrid = document.getElementById('locatorsGrid');
    if (locatorsGrid) {
        locatorsGrid.innerHTML = renderLocatorCards(filteredData);
        
        // Announce the change for screen readers
        const announcement = document.createElement('div');
        announcement.setAttribute('role', 'status');
        announcement.setAttribute('aria-live', 'polite');
        announcement.textContent = `Showing locations for ${metropolis}`;
        document.body.appendChild(announcement);
        setTimeout(() => announcement.remove(), 3000);
    }
    
    // Update active filter buttons
    const filterButtons = document.querySelectorAll('.filter-button');
    filterButtons.forEach(button => button.classList.remove('active'));
}

function closeMetropolisModal() {
  const modal = document.getElementById('metropolisSelectionModal');
  if (modal) {
    modal.style.opacity = '0';
    modal.style.transform = 'scale(0.9)';
    
    // Improved exit animation with callback
    setTimeout(() => {
      modal.remove();
      // Return focus to the element that opened the modal
      document.querySelector('[data-metropolis-trigger]')?.focus();
    }, 300);
  }
}

// Helper function to escape HTML special characters
function escapeHTML(str) {
  const div = document.createElement('div');
  div.textContent = str;
  return div.innerHTML;
}

function filterLocators(value, filterType = 'category') {
  // Remove active class from all filter buttons
  const filterButtons = document.querySelectorAll('.filter-button');
  filterButtons.forEach(button => button.classList.remove('active'));

  // Add active class to the clicked button
  const activeButton = document.querySelector(`.filter-button[data-category="${value}"]`);
  if (activeButton) activeButton.classList.add('active');

  // Filter locators
  const locatorsGrid = document.getElementById('locatorsGrid');
  const filteredData = value === 'All' 
    ? locatorsData 
    : locatorsData.filter(loc => loc[filterType] === value);

  // Update grid with filtered results
  locatorsGrid.innerHTML = renderLocatorCards(filteredData);
}

function hideLocatorsOverlay() {
  const overlay = document.getElementById('locatorsOverlay');
  if (overlay) {
    overlay.classList.remove('active');
    setTimeout(() => overlay.remove(), 300);
  }
}

// Additional placeholder functions (you might want to implement these)
function selectLocator(category) {
  console.log(`Selected locator in category: ${category}`);
}

function selectLocator(category) {
  // Optional: Add any specific action when a locator card is clicked
  console.log(`Selected locator in category: ${category}`);
}

document.addEventListener('DOMContentLoaded', function () {
  // Attach click event to the div with class "nav-item" and data-page="brand"
  const brandNavItem = document.querySelector('.nav-item[data-page="brand"]');
  if (brandNavItem) {
    brandNavItem.addEventListener('click', function (e) {
      e.preventDefault();
      showLocatorsOverlay();
    });
  }
});

function submitBookingViaWhatsApp() { const name = document.getElementById('nameInput').value.trim(); const contact = document.getElementById('contactInput').value.trim(); const address = document.getElementById('addressInput').value.trim(); const pincode = document.getElementById('pincodeInput').value.trim(); const date = document.getElementById('dateInput').value.trim(); const time = document.getElementById('timeInput').value.trim(); const bookingForm = document.getElementById('bookingForm'); const categoryId = bookingForm.dataset.categoryId || 'Not Specified'; const serviceName = bookingForm.dataset.serviceName || 'Not Specified'; const packageType = bookingForm.dataset.packageType || 'Not Specified'; if (!name || !contact) { showAlert('Please fill in Name and Contact Number', 'error'); return; } const message = `New Booking Request:\n📋 Category: ${categoryId}\n🛠 Service: ${serviceName}\n💎 Package: ${packageType}\n👤 Name: ${name}\n📞 Contact: ${contact}\n🏠 Address: ${address || 'Not Provided'}\n📍 Pincode: ${pincode || 'Not Provided'}\n📅 Date: ${date}\n⏰ Time: ${time}\n\nPlease confirm and process this booking.`; const encodedMessage = encodeURIComponent(message); const whatsappNumber = '78698 09022'; const whatsappUrl = `https://wa.me/${whatsappNumber.replace(/\s/g, '')}?text=${encodedMessage}`; window.open(whatsappUrl, '_blank'); showBookingConfirmation(); } function showBookingConfirmation() { const confirmationModal = document.createElement('div'); confirmationModal.id = 'bookingConfirmation'; confirmationModal.className = 'modal-overlay'; confirmationModal.innerHTML = `<div class="modal-content"><div class="confirmation-icon"><i class="fas fa-check-circle"></i></div><h2>Booking Submitted!</h2><p>Your booking request has been sent to WhatsApp. Our team will contact you shortly.</p><button onclick="closeConfirmation()" class="action-button">Close</button></div>`; document.body.appendChild(confirmationModal); document.getElementById('bookingForm').reset(); } function closeConfirmation() { const confirmationModal = document.getElementById('bookingConfirmation'); if (confirmationModal) { confirmationModal.remove(); } } document.addEventListener('DOMContentLoaded', function() { const submitBookingButton = document.getElementById('submitBooking'); if (submitBookingButton) { submitBookingButton.addEventListener('click', submitBookingViaWhatsApp); } }); document.addEventListener('DOMContentLoaded', function() { const locationNav = document.querySelector('.nav-item[data-page="location"]'); if (locationNav) { locationNav.addEventListener('click', function(e) { e.preventDefault(); showCitiesOverlay(); }); } }); function showAlert(message, type = 'success') { const alert = document.createElement('div'); alert.className = `alert alert-${type}`; alert.textContent = message; document.body.appendChild(alert); setTimeout(() => { alert.remove(); }, 3000); } function setupEventListeners() { window.addEventListener('click', function(event) { if (event.target.classList.contains('modal-overlay')) { closePackageInfo(); closeBookingForm(); closeConfirmation(); } }); }
                            </script>
                            
