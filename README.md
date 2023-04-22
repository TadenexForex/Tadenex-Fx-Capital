# Tadenex-Fx-Capital
{% extends 'customer/layouts/base.html' %}
{% load static %}
{% load humanize %}
{% load widget_tweaks %}
{% block content %}

	<!-- Breadcrumb -->
	<div class="breadcrumb-bar">
		<div class="container-fluid">
			<div class="row align-items-center">
				<div class="col-md-12 col-12">
					<nav aria-label="breadcrumb" class="page-breadcrumb">
						<ol class="breadcrumb">
							<li class="breadcrumb-item"><a href="{% url 'home:index' %}">Home</a></li>
							<li class="breadcrumb-item active" aria-current="page">Checkout</li>
						</ol>
					</nav>
					<h2 class="breadcrumb-title">Checkout</h2>
				</div>
			</div>
		</div>
	</div>
	<!-- /Breadcrumb -->

	<!-- Page Content -->
	<div class="content">
		<div class="container">

			<div class="row">
				<div class="col-md-7 col-lg-8">
					<div class="card">
						<div class="card-body">

							<!-- Checkout Form -->
							<form action="{% url 'customer:checkout_pay' %}" method="post" id="checkout">
								{% csrf_token %}
								<div class="payment-widget">
									<h4 class="card-title">Mpesa Payment</h4>
									<!-- Credit Card Payment -->
									<div class="payment-list">
										<label class="payment-radio credit-card-option">
											PayBill 877877
										</label>
										<div class="row">
											<div class="col-md-12">
												<div class="form-group card-label">
													<label>Phone Number</label>
													{% render_field form.phone class+="form-control" placeholder="+254702000000" %}
												</div>
												<div id="error-phone" class="text-danger"></div>
											</div>
											<div class="col-md-12">
												<div class="form-group card-label">
													<label>Mpesa Code</label>
													{% render_field form.mpesa class+="form-control" placeholder="MKDIR54ERW" %}
												</div>
												<div id="error-mpesa" class="text-danger"></div>
											</div>
											<div class="col-md-12">
												<div class="form-group card-label">
													<p> <b>Amount required:</b> Ksh.{{order.get_cart_total|floatformat:2|intcomma}}</p>
													<label>amount</label>
													{% render_field form.amount class+="form-control" placeholder="1000" %}
												</div>
												<div id="error-amount" class="text-danger"></div>
											</div>
										</div>
									</div>
									<!-- /Credit Card Payment -->
									<!-- Submit Section -->
									<div class="submit-section mt-4">
										<button type="submit" class="btn btn-primary submit-btn" id="checkout-btn">Confirm and Pay</button>
									</div>
									<!-- /Submit Section -->

								</div>
							</form>
							<!-- /Checkout Form -->

						</div>
					</div>

				</div>

				<div class="col-md-5 col-lg-4 theiaStickySidebar">

					<!-- Booking Summary -->
					<div class="card booking-card">
						<div class="card-header">
							<h4 class="card-title">Order Summary</h4>
						</div>
						<div class="card-body">
							<div class="booking-summary">
								<div class="booking-item-wrap">
<!--									<ul class="booking-date">-->
<!--										<li>Date <span>16 Nov 2019</span></li>-->
<!--										<li>Time <span>10:00 AM</span></li>-->
<!--									</ul>-->
									<ul class="booking-fee">
										{% for object in object_list %}
										<li>{{object.product.name}} <span>Ksh.{{object.get_total|floatformat:2|intcomma}}</span></li>
										{% endfor %}
									</ul>
									<div class="booking-total">
										<ul class="booking-total-list">
											<li>
												<span>Total</span>
												<span class="total-cost">Ksh.{{order.get_cart_total|floatformat:2|intcomma}}</span>
											</li>
										</ul>
									</div>
								</div>
							</div>
						</div>
					</div>
					<!-- /Booking Summary -->

				</div>
			</div>

		</div>

	</div>
	<!-- /Page Content -->

	{% endblock content %}
{% block scripts %}
	<!-- jQuery -->
	<script src="{% static 'customer/assets/js/jquery.min.js' %}"></script>

	<!-- Bootstrap Core JS -->
	<script src="{% static 'customer/assets/js/popper.min.js' %}"></script>
	<script src="{% static 'customer/assets/js/bootstrap.min.js' %}"></script>

	<!-- Sticky Sidebar JS -->
	<script src="{% static 'customer/assets/plugins/theia-sticky-sidebar/ResizeSensor.js' %}"></script>
	<script src="{% static 'customer/assets/plugins/theia-sticky-sidebar/theia-sticky-sidebar.js' %}"></script>

	<!-- Custom JS -->
	<script src="{% static 'customer/assets/js/script.js' %}"></script>
	<script src="{% static 'customer/assets/js/pay-product.js' %}"></script>
